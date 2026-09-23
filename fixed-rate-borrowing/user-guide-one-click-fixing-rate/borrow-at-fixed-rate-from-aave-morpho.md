---
description: >-
  Hedge an Aave loan’s floating borrowing costs with a long rates position on Rates Exchange.
---

# Borrow at a Fixed Rate

<a id="borrow-at-fixed-rate-from-aave-morpho"></a>

Keep your loan and collateral on Aave while hedging its floating borrowing cost through the **Hedge flow on Rates Exchange**.

Your long rates position pays fixed upfront and receives floating payments over the chosen term to offset your Aave borrowing costs. The loan and hedge remain separate positions.

## Get started

<a id="fixed-rate-borrowing-from-aave-morpho"></a>
<a id="borrow-on-aave-morpho"></a>

1. **Borrow on Aave:** Use a supported borrowing market and maintain the required loan collateral.

<a id="select-tenor-for-fixing-rate"></a>

2. **Choose your hedge:** Review the matching rates market, position size, fixed rate, expiry, upfront payment, and fees.

<a id="enter-long-rate-position"></a>

3. **Open the long:** Confirm through the Hedge flow. If your funding account and L2 wallet balances are insufficient, it automatically triggers bridging of the required funds from Ethereum mainnet. Your Aave collateral stays on Aave.

## Manage your position

- **Liquidation:** Your Rates Exchange long **cannot be liquidated** because its fixed obligation is paid upfront. Your Aave loan can still be liquidated, so continue monitoring its collateral and health.
- **Repayment:** Repay the loan through Aave. Repayment does not close the hedge; review its size whenever your borrowing changes.

<a id="manage-or-exit-early-optional"></a>

- **Early exit:** Close the long before expiry at available market terms. Fees and the exit price affect your result. Closing through the Hedge flow automatically bridges the remaining funds to your Ethereum mainnet wallet; it does not repay your Aave loan.

<a id="settlement-at-expiry"></a>
<a id="auto-rolling-optional"></a>

- **Expiry:** The hedge settles at the end of its term. Any unpaid Aave loan continues at its floating rate. **Auto-roll is upcoming and is not currently available.**

Your effective borrowing cost depends on the hedge’s size and term, fees, and floating payments received. Reduced receipts can leave some borrowing costs unhedged. See [Risks & Trust Assumptions](../../security/risks-and-trust-assumptions.md).

## Further reading

- [Fund & Withdraw](../../get-started/fund-and-withdraw.md)
- [PnL](../../rates-trading/payments-and-pnl.md)
- [Fees](../../rates-trading/fee.md)
