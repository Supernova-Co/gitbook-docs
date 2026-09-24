# Liquidation & Loss Allocation

A short can become liquidatable when its remaining collateral no longer meets the market's maintenance requirement. The protocol can then transfer the exposure to a funded participant or close it through market execution. If collateral and market backing are insufficient, separate loss-allocation rules determine who bears the shortfall.

## Two ways to resolve an unhealthy short

| Route | Who can initiate it? | What happens to the exposure? |
| --- | --- | --- |
| **Foreclosure: take over a position** | Anyone, while foreclosure is enabled and the transaction passes the required checks | The caller takes over an eligible share of the short and its allocated collateral, adds capital, and becomes responsible for that exposure. |
| **Liquidation: force a market close** | An account with the Manager's `LIQUIDATOR_ROLE` | The position is closed through the available order-book and vAMM route. The caller does not keep the short exposure. |

Both routes require an eligible short and execute without the holder’s approval.

<a id="liquidation"></a>

## When does a short become eligible?

A short becomes eligible when **LTV exceeds the market’s maintenance threshold**. See [Collateral Accounting](position-health.md#initial-and-maintenance-collateral) for the debt, collateral, and LTV calculations, and [Implied Rate & Mark Rate](vamm/README.md#collateral-and-liquidation) for the price inputs.

**Liquidatable does not necessarily mean insolvent.** A short can breach its maintenance threshold while still having enough collateral to cover its marked debt. The purpose of intervention is to address that risk before the backing is exhausted.

Longs are not subject to short-collateral liquidation. Funding shortfalls and recovery can reduce their payments or exposure, as described below.

Liquidation and foreclosure are available only before market maturity. After maturity, the market follows its expiry and settlement rules.

<a id="standard-flow"></a>

## Shared checks before either route

1. **Cancel the target's resting orders.** Release the collateral reserved for them.
2. **Account for accrued floating payments.** Update the position's `base` balance before assessing health. Accrual can reveal a shortfall that was absent from the stored balance.
3. **Check eligibility.** Revert if the short does not breach the required health condition.

Order cancellation and eligibility checks execute atomically; a failed eligibility check reverts the cancellation.

<a id="foreclosure-flow"></a>

## Foreclosure: anyone can take over eligible exposure

Foreclosure transfers exposure rather than immediately trading it away. The caller receives the selected portion of the short and its allocated collateral, including the applicable incentive, and supplies additional capital. The caller's resulting combined position must pass the stricter opening or modification health check.

The documented configuration uses **10–25% slices**, with **full takeover only for zero-equity positions**. The deployed market configures `isForeclosureAllowed`, size limits, and incentive settings.

The caller assumes the acquired short’s floating obligations. The takeover involves no forced vAMM trade; a later close incurs execution fees and price impact.

### Takeover accounting

The following **accounting pseudocode** describes the transfer, rather than a callable ABI. `allocatedBase` includes the collateral and incentive assigned by the foreclosure rules; incentive sourcing and rounding are omitted.

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

After the shared checks, an authorized liquidator closes some or all of the short through the available order-book and vAMM route. The target's collateral funds the close, and the configured liquidation charges apply. Any uncovered closing shortfall is recorded against the vault.

The caller receives the configured liquidation reward without retaining the short. Execution fees and price impact apply. Venue capacity can require a large position to be closed through multiple calls.

## How losses are allocated

Closing shortfalls, funding shortfalls, and exhausted backing trigger the following loss-allocation mechanisms.

### 1. Closing shortfalls reduce vault backing

If the close cannot recover the amount owed, `accrueBadDebt` records the uncovered loss against the vault. LPs bear the reduction through the value backing their shares.

Recorded vault assets are floored at zero.

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

<a id="matched-recovery"></a>

### 3. Recovery can reduce long exposure

The market enters one-way matched recovery mode if an epoch requires `φ < 1`, or if negative vault PnL exhausts its backing. Before maturity, entry into recovery trims the unmatched long exposure pro rata, leaving a 1:1 matched book. The vAMM is disabled and vault deposits are restricted.

**Risk valuation:** Liquidation eligibility in matched recovery uses the **forward mark** instead of the normal vAMM TWAP. The current forward-rate input is the oracle-supplied floating rate, converted into a price for the remaining term:

```text
Forward mark price = Floating APR × Remaining duration in days / 365
```

Matched recovery is the market mode; ADL is a position-reduction mechanism within that mode.

**Auto-deleveraging (ADL)** reduces long positions pro rata when a distressed short is terminated in matched mode. Longs receive the short’s remaining collateral; the payout is based on available collateral rather than a TWAP-priced close.

The mechanism reference identifies this internal call path:

```text
Manager.liquidate()                 # requires LIQUIDATOR_ROLE
  -> Manager._terminateShort()      # internal matched-mode branch
     -> vault.distributeBaseToLongs()
     -> vault.writeOffTrim()
```

`_terminateShort()` is an internal branch of the role-restricted liquidation path. The recovery latch is evaluated during transactions calling `Vault.settleFunding`.

## What anyone can do

- **Monitor and manage their position:** See [Managing Collateral](../rates-trading/interactive-blocks.md) for health and collateral actions.
- **Participate in foreclosure** when enabled, by taking eligible exposure and supplying enough capital to pass the combined-position health check.

Forced liquidation and parameter changes retain their respective role restrictions.

## Further reading

- [Managing Collateral](../rates-trading/interactive-blocks.md)
- [Collateral Accounting](position-health.md)
- [Settlement](vamm/settlement-accrual.md)
- [Vault Guardrails](vault/vault-guardrails.md)
- [Risks & Trust Assumptions](../security/risks-and-trust-assumptions.md)
