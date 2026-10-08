# Liquidation & Loss Allocation

A short can become liquidatable when its remaining collateral no longer meets the market's maintenance requirement. Whitelisted accounts then resolve it by taking it over, closing it through the market, or in an extreme scenario closing it against the longs. If collateral and market backing are insufficient, separate loss-allocation rules determine who bears the shortfall.

## Three ways to resolve an unhealthy short

| Route | Who can use it? | What happens to the short? |
| --- | --- | --- |
| **Foreclosure** | Whitelisted accounts initially, such as the insurance fund | Taken over: the caller assumes part of the short and its debt. |
| **Liquidation** | Whitelisted liquidators | Closed through the order book and vAMM, with the vault as backstop. |
| **Auto-deleveraging (ADL)** | Whitelisted liquidators | Closed against all longs, pro rata. |

All three execute without the holder's approval. Rates Exchange runs liquidation bots that monitor position health, including floating payments not yet written to balances (see [lazy settlement](vamm/settlement-accrual.md#lazy-settlement)).

<a id="liquidation"></a>

## When does a short become eligible?

A short becomes eligible when **LTV exceeds the market’s maintenance threshold**. See [Collateral Accounting](position-health.md#initial-and-maintenance-collateral) for the debt, collateral, and LTV calculations, and [Implied Rate & Mark Rate](vamm/README.md#collateral-and-liquidation) for the price inputs.

**Liquidatable does not necessarily mean insolvent.** A short can breach its maintenance threshold while still having enough collateral to cover its marked debt. The purpose of intervention is to address that risk before the backing is exhausted.

Longs cannot be liquidated: their fixed payments for the full term are known and locked at entry, so they owe nothing further. Auto-deleveraging and matched recovery can still reduce their exposure, as described below.

Liquidation is available only before market maturity. After maturity, the market follows its expiry and settlement rules.

<a id="standard-flow"></a>

## Shared checks before any route

1. **Cancel the target's resting orders.** Release the collateral reserved for them.
2. **Account for accrued floating payments.** Update the position's `base` balance before assessing health. Accrual can reveal a shortfall that was absent from the stored balance.
3. **Check eligibility.** Revert if the short does not breach the required health condition.

Order cancellation and eligibility checks execute atomically; a failed eligibility check reverts the cancellation.

<a id="liquidation-flow"></a>

## Liquidation: close through the market

An authorized liquidator closes some or all of the short through the available order-book and vAMM route, with the vault taking the other side of vAMM fills. The liquidator does not keep the short exposure. The target's collateral funds the close. Any uncovered closing shortfall is recorded against the vault.

Execution fees and price impact apply. Venue capacity can require a large position to be closed through multiple calls.

<a id="liquidation-bonus"></a>

### Liquidation penalty

The liquidation penalty is **1% of the total position sold**. The liquidator receives 10% of the penalty. Of the rest, 90% goes to the vault and 10% to the protocol.

**Example:** If a liquidation sells $10,000 of a position, the penalty is $100: $10 goes to the liquidator, $81 to the vault, and $9 to the protocol.

The penalty is paid from the position's remaining collateral and is limited to what remains. Any collateral left after the close and penalty stays in the position's isolated account.

<a id="foreclosure-flow"></a>

## Foreclosure: take over the position

Foreclosure transfers part of the short to the caller instead of trading it away. It is **whitelisted initially**.

The caller takes on a share of the short's notional and its debt. In return, it receives collateral worth that debt at the mark, plus a **premium of 25% of that share's equity**. The rest of that share's equity stays with the position holder. A foreclosure takes 10–25% of the position, or all of it; a position with no equity left can only be taken over in full. The caller's resulting combined position must pass the stricter opening health check.

**Example:** A short with $100,000 notional has $1,500 of collateral and $1,000 of debt at the mark, so its equity is $500. The insurance fund forecloses 20%: it takes on $20,000 notional and $200 of debt. That share's equity is $100, so the fund receives $200 + 25% × $100 = **$225** of collateral. The other $75 of that equity stays with the holder, whose position is now $80,000 notional with $1,275 of collateral and $800 of debt.

The caller assumes the acquired short's floating obligations. The takeover involves no mandatory vAMM or order-book trade.

The insurance fund uses part of its funds to take over distressed positions through foreclosure before they reach ADL.

<a id="adl"></a>

## Auto-deleveraging (ADL)

Liquidating through the market can always be used, but repeatedly draining the vault to absorb liquidations weakens the market. Once the vault has already absorbed significant losses in a market and the insurance fund is depleted, a whitelisted liquidator can use ADL instead for a short whose LTV is close to 100%.

ADL closes the whole short against every long, pro rata. Each long's position is reduced by its share of the short's notional, and each long receives the same share of the short's collateral, up to the value of its debt at the mark (the TWAP mark rate, or the 3-day moving average in matched recovery). Any collateral above that is returned to the short's owner. No liquidation penalty applies.

- **At 100% LTV**, the short's collateral exactly matches its debt at the mark, so longs are closed at the mark.
- **Above 100% LTV**, there is less collateral than the debt is worth, so longs are closed at a worse price than the mark.

The decision that the vault has absorbed enough losses and the insurance fund is depleted is made by the liquidation bots, not on-chain. In [matched recovery](vault/vault-guardrails.md#matched-recovery), ADL is the only route for liquidating a short.

The mechanism reference identifies this internal call path:

```text
Manager.liquidate()                 # requires LIQUIDATOR_ROLE
  -> Manager._terminateShort()      # write-off branch
     -> vault.distributeBaseToLongs()
     -> vault.writeOffTrim()
```

## How losses from underwater shorts are recovered

A short is underwater when its collateral no longer covers its debt at the mark. The shortfall is covered in this order:

1. **The position's own collateral.** Foreclosure, liquidation, or ADL uses whatever collateral remains.
2. **The vault.** If a close through the market cannot recover the amount owed, `accrueBadDebt` records the uncovered loss against the vault.
3. **The insurance fund.** It takes over distressed positions through foreclosure before they reach ADL.
4. **Longs, through ADL.** Once the vault has absorbed significant losses and the insurance fund is depleted, ADL closes the short against the longs.

<a id="insurance-fund"></a>

### The insurance fund

A share of protocol fees is set aside as a protocol-level insurance fund. It takes over distressed positions through foreclosure before they reach ADL, and protects users in case of a hack. Because it pools fees across all markets and over time, it can cover losses larger than a single market's fees.

## What you can do

Keep a short healthy by adding collateral or reducing exposure. See [Managing Collateral](../rates-trading/interactive-blocks.md) for health and collateral actions.


## Further reading

- [Managing Collateral](../rates-trading/interactive-blocks.md)
- [Collateral Accounting](position-health.md)
- [Settlement](vamm/settlement-accrual.md)
- [Vault Guardrails](vault/vault-guardrails.md)
- [Risks & Trust Assumptions](../security/risks-and-trust-assumptions.md)
