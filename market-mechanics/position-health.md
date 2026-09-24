# Collateral Accounting

A rates account tracks available funds, position balances, and order reservations.

## Account concepts

| Concept | Meaning |
| --- | --- |
| Available balance | Funds not currently committed to a position or order |
| Position balance | Funds accounted for within a market position |
| Signed notional | The size and direction of rate exposure |
| Order reservation | Funds or exposure committed to a resting order |

In existing notation, `base` records a position balance and `quote` records signed notional. Positive notional denotes long exposure; negative notional denotes short exposure. Order reservations reduce available collateral or exposure.

Position balances change through trade cash flows, floating settlement, and collateral transfers. See [PnL](../rates-trading/payments-and-pnl.md) for cash flows and [Settlement](vamm/settlement-accrual.md) for accrual accounting.

## Initial and maintenance collateral

For a short, the debt value represents the cost assigned to closing its remaining exposure:

```text
Debt value = absolute notional × price per unit of notional
LTV = debt value / eligible collateral
```

The notional and price must use consistent units. LTV rises when the valued obligation increases or eligible collateral decreases. Higher LTV means less backing relative to the obligation.

| Check | Valuation | Eligible collateral |
| --- | --- | --- |
| Open or modify a short | The highest of the time-weighted mark, spot price, and applicable price floor | Position balance less funds reserved for orders |
| Liquidation condition | Time-weighted mark in normal mode; forward mark in matched recovery | Position balance after orders are cancelled and accrued payments are accounted for |

The opening check uses a stricter safe LTV than the maintenance threshold. The safe threshold is a fraction of the maintenance threshold, leaving a buffer between opening a position and becoming liquidatable.

### Floor margin

A minimum margin requirement ensures that positions opened in the final **5 days before maturity cannot be liquidated**. The floor applies to opening and modification checks; it does not raise the liquidation threshold.

## Withdrawals

See [Managing Collateral](../rates-trading/interactive-blocks.md#adding-or-withdrawing-collateral) for withdrawal health checks and [Orders & Execution](order-book.md#withdrawals) for open-order restrictions.

<a id="position-health"></a>
<a id="health-ratio"></a>
<a id="two-ltv-thresholds"></a>
<a id="funding-erodes-collateral-first"></a>
