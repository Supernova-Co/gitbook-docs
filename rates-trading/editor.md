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

# Long vs Short

Both sides trade the same underlying rate and expiry. Their payment obligations are different.

| | Long | Short |
| --- | --- | --- |
| Fixed obligation | Pays upfront | Receives upfront |
| Floating payments | Receives | Pays |
| Typical use | Hedge a floating borrowing cost or express a view on rising rates | Hedge floating lending income or express a view on falling rates |
| Position funding | Funds the fixed obligation | Provides collateral for future obligations |
| Liquidation exposure | No unpaid fixed obligation after prepayment | Can become liquidatable as collateral becomes insufficient |

## Rate exposure

A rise in the implied rate generally improves a long's exit value and worsens a short's. A fall generally has the opposite effect. Meanwhile, floating payments accrue according to the underlying rate.

These effects must be considered together with the remaining term and costs. A favorable rate move does not by itself establish total profit.

## Trading or hedging

You can trade rates without creating a loan or deposit in the underlying protocol. When using a hedge, the underlying loan or deposit remains separate from the Rates Exchange position.

For a lender, differences between supply yield and the rate paid by the short can leave residual exposure. For a borrower, the hedge's size and term need to be considered against the loan.

## Risks

A short can lose collateral through floating payments and unfavorable changes in the cost of closing. A prepaid long still has market and protocol risk, including the risk of reduced floating receipts.

See [Payments & PnL](payments-and-pnl.md), [Borrow at a Fixed Rate](../fixed-rate-borrowing/user-guide-one-click-fixing-rate/borrow-at-fixed-rate-from-aave-morpho.md), and [Lend with Yield Boost](../fixed-rate-borrowing/fixed-rate-yield-boost/README.md).

<a id="long-rate"></a>
