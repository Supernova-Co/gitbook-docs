---
description: >-
  Hedge an Aave loan’s floating borrowing costs with a long rates position on Rates Exchange.
---

# Borrow at a Fixed Rate

<a id="borrow-at-fixed-rate-from-aave-morpho"></a>

Keep your loan and collateral on Aave while hedging its floating borrowing cost through the **Hedge flow on Rates Exchange**.

Your long rates position locks in its full fixed payment for the term at entry and receives floating payments over that term to offset your Aave borrowing costs.

## Get started

<a id="fixed-rate-borrowing-from-aave-morpho"></a>
<a id="borrow-on-aave-morpho"></a>

1. **Borrow on Aave:** Use a supported borrowing market and maintain the required loan collateral.

<a id="select-tenor-for-fixing-rate"></a>

2. **Choose your hedge:** Review the matching rates market, position size, fixed rate, expiry, fixed payment, and fees.

<a id="enter-long-rate-position"></a>

3. **Open the long:** Confirm through the Hedge flow. If your funding account and L2 wallet balances are insufficient, it automatically triggers bridging of the required funds from Ethereum mainnet. Your Aave collateral stays on Aave.

## Example

You borrow **100,000 USDC** on Aave at a floating rate and hedge it with a **100,000 notional** long at a **5% fixed rate**, with **30 days** until expiry. The fixed payment for the term is locked at entry:

```text
Fixed payment = 100,000 × 5% × 30 / 365 = $410.96
```

Over the 30 days, the long receives floating payments at the Aave borrow rate, offsetting the interest your loan accrues:

| | Borrow rate averages 7% | Borrow rate averages 3% |
| --- | --- | --- |
| Aave interest owed | $575.34 | $246.58 |
| Floating payments received by the long | −$575.34 | −$246.58 |
| Fixed payment locked at entry | $410.96 | $410.96 |
| **Net borrowing cost** | **$410.96 (5%)** | **$410.96 (5%)** |

Whether rates rise or fall, your borrowing cost stays at the 5% fixed rate, before fees.

## Manage your position

- **Liquidation:** Your Rates Exchange long **cannot be liquidated**: its fixed payments for the full term are known and locked at entry, so it owes nothing further. Your Aave loan can still be liquidated, so continue monitoring its collateral and health.
- **Repayment:** Repay the loan through Aave. Repayment does not close the hedge; review its size whenever your borrowing changes.

<a id="manage-or-exit-early-optional"></a>

- **Early exit:** Close the long before expiry at available market terms. Fees and the exit price affect your result. Closing through the Hedge flow automatically bridges the remaining funds to your Ethereum mainnet wallet; it does not repay your Aave loan.

<a id="settlement-at-expiry"></a>
<a id="auto-rolling-optional"></a>

- **Expiry:** Floating payments stop at the end of the term. The hedge's remaining balance is not returned automatically; [withdraw it](../../rates-trading/payments-and-pnl.md#at-expiry) yourself. Any unpaid Aave loan continues at its floating rate. **Auto-roll is upcoming and is not currently available.**

Your effective borrowing cost depends on the hedge’s size and term, fees, and floating payments received. In extreme market conditions, [Auto-deleveraging](../../market-mechanics/liquidation.md#adl) or [matched recovery](../../market-mechanics/vault/vault-guardrails.md#matched-recovery) can reduce your long, leaving some borrowing costs unhedged. See [Risks & Trust Assumptions](../../security/risks-and-trust-assumptions.md).

{% hint style="warning" %}
**Your Aave loan and your Rates Exchange hedge are independent positions.** Repaying, increasing, or refinancing the loan does not close or resize the hedge, and closing the hedge does not repay the loan. Review the hedge's size whenever your borrowing changes.
{% endhint %}

## Further reading

- [Fund & Withdraw](../../get-started/fund-and-withdraw.md)
- [PnL](../../rates-trading/payments-and-pnl.md)
- [Fees](../../rates-trading/fee.md)
