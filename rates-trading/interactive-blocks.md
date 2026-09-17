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

A short receives fixed upfront and pays floating over time. Keep enough collateral in its isolated market account to support those obligations. Funds in your wallet, funding account, or another market do not back the short.

## Monitor position health

- **Floating payments:** Accrued payments reduce the short's collateral over time.
- **Rate changes:** A higher implied rate can increase the cost of closing the short and weaken its health.
- **Open orders:** Reserved funds affect the amount available for trading or withdrawal.

Health can deteriorate even when the quoted fixed rate is unchanged. Monitor accrued payments as well as the displayed balance.

## Add collateral or reduce exposure

Add collateral to the relevant isolated account to increase the funds backing the short. Alternatively, close part or all of the position to reduce its remaining exposure. Closing depends on available execution and incurs applicable fees.

Opening or modifying a short requires a buffer above the liquidation condition. Use the market's opening requirement when sizing a position. See [Collateral Accounting](../market-mechanics/position-health.md) for the valuation and health checks.

## Withdraw available collateral

Check the available amount and the short's resulting health before withdrawing. Funds reserved for orders or needed to support the position are not freely withdrawable. See [Fund & Withdraw](../get-started/fund-and-withdraw.md).

<a id="liquidation-threshold"></a>

## If health falls below the requirement

An eligible short may be taken over through foreclosure or closed through liquidation. Act before it reaches that condition by adding collateral or reducing exposure. See [Liquidation & Loss Allocation](../market-mechanics/liquidation.md) for eligibility, caller permissions, and loss allocation.

A long rates position cannot be liquidated because its fixed obligation is paid upfront. It still carries market and payment-shortfall risk. Any underlying loan has its own collateral and liquidation requirements.
