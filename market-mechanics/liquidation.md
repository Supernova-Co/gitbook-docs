# Liquidation & Loss Allocation

A short can become liquidatable when its remaining collateral no longer meets the market's maintenance requirement. The protocol can then transfer the exposure to a funded participant or close it through market execution. If collateral and market backing are insufficient, separate loss-allocation rules determine who bears the shortfall.

## Two ways to resolve an unhealthy short

| Route | Who can initiate it? | What happens to the exposure? |
| --- | --- | --- |
| **Foreclosure: take over a position** | Anyone, while foreclosure is enabled and the transaction passes the required checks | The caller takes over an eligible share of the short and its allocated collateral, adds capital, and becomes responsible for that exposure. |
| **Liquidation: force a market close** | An account with the Manager's `LIQUIDATOR_ROLE` | The position is closed through the available order-book and vAMM route. The caller does not keep the short exposure. |

Foreclosure is the permissionless liquidation mechanism. That does **not** make every function named `liquidate()` permissionless: the Manager's forced-close path is role-restricted.

Neither route requires the short holder's approval once the position is eligible. Neither can be used to seize a healthy position.

<a id="liquidation"></a>

## When does a short become eligible?

A short receives fixed upfront and pays floating over time. Its health can deteriorate because the market value of its remaining obligation rises, because accrued floating payments reduce its collateral, or both.

```text
Debt value = absolute short notional × risk price
LTV = debt value / eligible collateral
Liquidation condition: LTV > maintenance LTV
```

These equations assume consistent notional, price, and collateral units. Maintenance valuation uses the vAMM's time-weighted price in normal mode, or the forward mark in matched mode. Use the market's configured threshold rather than a universal percentage.

**Liquidatable does not necessarily mean insolvent.** A short can breach its maintenance threshold while still having enough collateral to cover its marked debt. The purpose of intervention is to address that risk before the backing is exhausted.

Longs prepay their fixed obligation, so they do not face this short-collateral liquidation process. They can still receive reduced floating payments or have exposure reduced during recovery. An underlying Aave or Morpho loan has its own liquidation rules.

Liquidation and foreclosure are available only before market maturity. After maturity, the market follows its expiry and settlement rules.

<a id="standard-flow"></a>

## Shared checks before either route

1. **Cancel the target's resting orders.** Release the collateral reserved for them.
2. **Account for accrued floating payments.** Update the position's `base` balance before assessing health. Accrual can reveal a shortfall that was absent from the stored balance.
3. **Check eligibility.** Revert if the short does not breach the required health condition.

Order cancellation is part of this checked transaction. Permissionless foreclosure does not give callers an unrestricted right to cancel another user's orders.

<a id="foreclosure-flow"></a>

## Foreclosure: anyone can take over eligible exposure

Foreclosure transfers exposure rather than immediately trading it away. The caller receives the selected portion of the short and its allocated collateral, including the applicable incentive, and supplies additional capital. The caller's resulting combined position must pass the stricter opening or modification health check.

The documented configuration uses **10–25% slices**, with **full takeover only for zero-equity positions**. Availability depends on `isForeclosureAllowed`; size limits and incentive settings should be checked against the deployed market.

The caller now owes the floating payments associated with the acquired short. They can hold the exposure or subsequently close it through an available execution route. That later close can incur fees and price impact, so the incentive is not a guaranteed profit.

The transfer itself avoids a forced vAMM trade. It does not eliminate the transferred position's risk or guarantee liquidity for a later exit.

### Takeover accounting

The following pseudocode explains the transfer. It is **not an executable contract call or a verified ABI**. `allocatedBase` includes the collateral and incentive assigned by the foreclosure rules; incentive sourcing and rounding are omitted.

```text
# Preconditions: before maturity, foreclosure enabled, target eligible.
# All balances include accrued payments; target orders are cancelled.

transferredQuote = target.quote * permittedSlice

caller.base  = caller.base + capitalInfusion + allocatedBase
caller.quote = caller.quote + transferredQuote

# The target's corresponding exposure and collateral are removed.
# Revert the whole transaction unless the caller's combined position
# satisfies the market's opening / modification health requirement.
```

In this notation, `base` is the accounted collateral balance and a negative `quote` is short notional. See [Collateral Accounting](position-health.md).

<a id="liquidation-flow"></a>

## Liquidation: an authorized caller closes the exposure

The forced-close route is a backstop when participants do not take over an unhealthy short, for example because keeping or unwinding the exposure is unattractive.

After the shared checks, an authorized liquidator closes some or all of the short through the available order-book and vAMM route. The target's collateral funds the close, and the configured liquidation charges apply. Any uncovered closing shortfall is recorded against the vault.

The caller receives the applicable liquidation reward without retaining the short. Unlike foreclosure, this route involves market execution and can create price impact. A call remains subject to venue capacity; a large position may require multiple calls.

Liquidation charges, execution fees, and price impact are separate costs. Use the deployed fee and reward settings when estimating proceeds.

## How losses are allocated

A liquidation trigger and a payment shortfall are different events. The following mechanisms address different kinds of shortfall; they are not a promise that every loss can be recovered.

### 1. Closing shortfalls reduce vault backing

If the close cannot recover the amount owed, `accrueBadDebt` records the uncovered loss against the vault. LPs bear the reduction through the value backing their shares.

A floor of zero on recorded vault assets prevents a negative accounting balance. It does not restore lost funds or guarantee payment to other participants.

### 2. Insufficient funding reduces long receipts

During settlement, the vault checks whether its remaining backing can fund the net floating payment owed to longs. If it cannot, the funding factor `φ` falls below 1. Longs share the available payment pro rata while shorts remain liable for their full floating payment and fee.

For an epoch in which the vault owes the difference:

```text
headroom = max(totalAssets + vaultPnL, 0)
netAmountOwedByVault = longPayments - shortPayments  # positive here
phi = min(1, headroom / netAmountOwedByVault)

availableForLongs = shortPayments + phi * netAmountOwedByVault
```

This is the funding calculation described in the mechanism reference, with fixed-point scaling omitted. `phi` scales the **vault-funded gap**, not necessarily all payments collected from shorts. A long's actual receipts can therefore be lower than its expected floating payment.

### 3. Recovery can reduce long exposure

The market enters one-way matched recovery mode if an epoch requires `φ < 1`, or if negative vault PnL exhausts its backing. Before maturity, entry into recovery trims the unmatched long exposure pro rata, leaving a 1:1 matched book. The vAMM is disabled and vault deposits are restricted.

Within matched mode, terminating a distressed short can also reduce long positions pro rata and distribute the short's remaining collateral. This is **auto-deleveraging (ADL)**. Longs receive the collateral available to distribute, not a guaranteed TWAP-priced close.

The mechanism reference identifies this internal call path:

```text
Manager.liquidate()                 # requires LIQUIDATOR_ROLE
  -> Manager._terminateShort()      # internal matched-mode branch
     -> vault.distributeBaseToLongs()
     -> vault.writeOffTrim()
```

These are implementation references, not standalone calls available to any user. The recovery latch is evaluated in `Vault.settleFunding`. Automatic checks run inside onchain transactions; they do not execute independently in the background.

## What anyone can do

- **Monitor position health**, including accrued payments and order reservations, rather than relying on a stored collateral balance alone.
- **Participate in foreclosure** when enabled, by taking eligible exposure and supplying enough capital to pass the combined-position health check.
- **Manage their own position** by adding collateral or closing exposure through the available routes before it becomes eligible for intervention.

Permissionless participation does not grant the right to call the restricted forced-close path, change risk parameters, bypass maturity or health checks, or withdraw another participant's collateral.

## Further reading

- [Managing Collateral](../rates-trading/interactive-blocks.md)
- [Collateral Accounting](position-health.md)
- [Settlement](vamm/settlement-accrual.md)
- [Vault Guardrails](vault/vault-guardrails.md)
- [Risks & Trust Assumptions](../security/risks-and-trust-assumptions.md)
