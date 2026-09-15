# Collateral Accounting

A rates account needs to distinguish available funds, funds backing positions, and amounts reserved for orders.

## Account concepts

| Concept | Meaning |
| --- | --- |
| Available balance | Funds not currently committed to a position or order |
| Position balance | Funds accounted for within a market position |
| Signed notional | The size and direction of rate exposure |
| Order reservation | Funds or exposure committed to a resting order |

In existing notation, `base` records a position balance and `quote` records signed notional. Positive notional denotes long exposure; negative notional denotes short exposure. Those fields alone do not explain available funds when orders are also present.

## What changes a position balance?

Fixed payments at execution, floating accrual, additions or removals of funds, and closing transactions affect the accounting. Order reservations additionally affect what can be committed elsewhere.

Accrual describes the economic amount earned or owed over time. Updating a stored balance is a separate accounting step. A balance snapshot must be interpreted together with outstanding accrual and reservations.

## Short obligations and health

A short's remaining obligation is valued using the market's risk rules. Health compares that obligation with the funds eligible to support it.

Opening or modifying a position and triggering liquidation are separate checks. Their applicable price, eligible collateral, and threshold should not be treated as interchangeable.

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
| Liquidation condition | Time-weighted mark | Position balance after orders are cancelled and accrued payments are accounted for |

The opening check uses a stricter safe LTV than the maintenance threshold. The safe threshold is a fraction of the maintenance threshold, leaving a buffer between opening a position and becoming liquidatable.

A price floor affects the opening or modification requirement near expiry; it is not a floor on the maintenance valuation.

## Withdrawals

A total balance is not the same as withdrawable funds. Open positions must remain supported, and resting orders can commit funds. Review available balance and position health before withdrawing.

For the user-facing explanation, see [Collateral, Health & Liquidation](../rates-trading/interactive-blocks.md). For shortfalls, see [Liquidation & Loss Allocation](liquidation.md).

<a id="position-health"></a>
<a id="health-ratio"></a>
<a id="two-ltv-thresholds"></a>
<a id="funding-erodes-collateral-first"></a>
