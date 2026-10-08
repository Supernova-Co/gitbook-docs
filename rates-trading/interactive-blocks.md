---
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Managing Collateral

Short positions require collateral in their isolated market account. Long positions cannot be liquidated: their fixed payments for the full term are known and locked at entry.

## What changes a short’s health?

- **Floating payments** reduce collateral over time, even if the quoted fixed rate stays unchanged.
- **A higher implied rate** can increase the short’s valued obligation and push it closer to liquidation.
- **Open orders** reserve funds, reducing the collateral available to support additional trades.

<a id="liquidation-threshold"></a>

## Opening and liquidation thresholds

Opening or modifying a short requires an LTV of at most **33%**, while a short becomes liquidatable only above **66%**. A short can therefore avoid liquidation but still lack enough collateral to increase exposure or withdraw funds.

Health checks use the market’s risk valuation, which can differ from the current execution price. See [Collateral Accounting](../market-mechanics/position-health.md) for the calculation.

## Adding or withdrawing collateral

Adding collateral improves the short’s health. Excess collateral can be withdrawn only if the remaining position passes the required health check.

**An open position does not lock the entire balance. Open orders, however, block withdrawals of any amount, including unreserved funds. Cancel all open orders before withdrawing.**

See [Orders & Execution](../market-mechanics/order-book.md#collateral-for-orders-and-positions) for reservation rules.

If the short breaches its maintenance requirement, it becomes eligible for [foreclosure, liquidation, or auto-deleveraging](../market-mechanics/liquidation.md).
