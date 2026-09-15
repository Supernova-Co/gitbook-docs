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

# Collateral, Health & Liquidation

A short receives a fixed payment at entry and owes floating payments over time. Its collateral must remain sufficient under the market's health rules.

## What changes health?

- A higher implied rate can increase the cost of closing a short.
- Floating payments can reduce the collateral remaining in the position.
- Adding funds, withdrawing funds, trading, or reserving funds for orders can change what is available to support the position.

A persistently high floating rate can weaken health even without a sharp move in the implied rate.

## Opening requirements and liquidation requirements

The requirement to open or modify a position is distinct from the condition that makes an existing position liquidatable. Do not use the liquidation threshold as a target for sizing a new position.

The market's risk price is also distinct from the price at which an order will execute. See [Pricing & Mark Rates](../market-mechanics/vamm/README.md).

## Managing collateral

Monitor accrued obligations alongside the balance shown for the position. Funds reserved for orders or required by open positions should not be assumed to be withdrawable.

Review the effect of a withdrawal on remaining health before removing funds. Closing exposure and adding collateral have different effects on the account.

## Liquidation

A short that fails the required health condition can be liquidated. Liquidation can reduce or close exposure and consume collateral, with applicable charges affecting what remains.

A long's prepaid fixed obligation does not remove risks in the underlying loan, or risks of market losses and reduced payments on Rates Exchange.

## Further reading

- [Collateral Accounting](../market-mechanics/position-health.md)
- [Liquidation & Loss Allocation](../market-mechanics/liquidation.md)
- [Risks & Trust Assumptions](../security/risks-and-trust-assumptions.md)

<a id="liquidation-threshold"></a>
