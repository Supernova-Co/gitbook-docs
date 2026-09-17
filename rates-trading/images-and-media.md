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

# Open Position

Opening a rates position creates exposure to a particular underlying rate and expiry. Check the notional, remaining term, execution terms, and funds required before submitting an order.

## Position funding

A long pays its fixed obligation upfront. A short receives the fixed payment and must provide sufficient collateral to back its future obligations. The fixed payment, total position collateral, and additional funds supplied by the user are different quantities.

The notional is the size of the rate exposure, not the amount transferred into the account.

## Orders and positions

An order becomes a position only when it executes. Resting orders can reserve funds or exposure, so funds committed to an order are not available for every other action.

For the walkthrough, see [Trade Rates](../user-guides/trade-rates.md). For reference, see [Supported Markets](../get-started/supported-markets.md), [Orders & Execution](../market-mechanics/order-book.md), and [Managing Collateral](interactive-blocks.md).
