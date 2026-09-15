---
description: >-
  Use a Rates Exchange long rate position alongside an Aave loan
  to hedge floating borrowing costs for a chosen term.
---

# Borrow at a Fixed Rate

<a id="borrow-at-fixed-rate-from-aave-morpho"></a>

## What it does

Rates Exchange lets you combine a floating-rate loan on Aave with a separate rates hedge. The hedge is designed to make borrowing costs more predictable for a chosen term while the loan remains in the underlying lending protocol.

## How it works

You manage two separate positions:

| Position | Where it lives | What it does |
| --- | --- | --- |
| Borrowing position | Aave | Pays the underlying market’s floating borrowing rate |
| Long rate position | Rates Exchange | Pays fixed and receives floating for a chosen term |

The long rate position is the hedge. Its floating receipts are intended to offset the borrowing cost of the underlying loan. The fixed-rate obligation is paid upfront when the rates position opens.

{% hint style="info" %}
The hedge does not replace your loan or its collateral requirements. Your Aave position remains subject to the underlying protocol’s rules and liquidation risk.
{% endhint %}

## How to use it

<a id="fixed-rate-borrowing-from-aave-morpho"></a>

{% stepper %}
{% step %}
### Start with a borrowing position

<a id="borrow-on-aave-morpho"></a>

Borrow through a supported Aave market. Manage the loan and its collateral under that protocol’s rules.
{% endstep %}

{% step %}
### Review the market and term

<a id="select-tenor-for-fixing-rate"></a>

Review the available rates market, quoted fixed rate, and term, also called its tenor. Consider the borrowing exposure you intend to hedge and the costs of opening the rates position.
{% endstep %}

{% step %}
### Open the long rate position

<a id="enter-long-rate-position"></a>

Provide the funds required for the Rates Exchange position. Enter the long: pay fixed and receive floating.

Keep track of both the underlying loan and the separate rates position.
{% endstep %}
{% endstepper %}

## Managing the position

### Collateral

Continue managing the collateral and health of your Aave loan. Funds required for the Rates Exchange position are separate from the collateral supporting that loan.

### Repaying the underlying loan

Use Aave’s repayment process for full or partial repayment. Review the hedge when the size of your borrowing changes. Treat repayment and closing the rates position as separate actions.

### Closing the hedge

<a id="manage-or-exit-early-optional"></a>

You can seek to close the Rates Exchange long before expiry. The outcome depends on the exit terms and execution. Any outstanding underlying loan continues at its floating borrowing rate without that hedge.

### Expiry

<a id="settlement-at-expiry"></a>
<a id="auto-rolling-optional"></a>

The rates position settles at the end of its term. Any unpaid Aave loan remains outstanding at its floating rate. Plan for the hedge to end. **Auto-roll is upcoming and is not currently available.**

## Risks and limitations

- **Underlying loan risk:** The hedge does not remove Aave’s collateral requirements or liquidation risk.
- **Separate hedge risk:** Using Rates Exchange adds a separate position and protocol exposure alongside the loan.
- **Hedge fit:** The rates market, position size, and term must be considered in relation to your borrowing exposure. Do not assume the hedge covers every borrowing cost.
- **Costs and exit:** Funding the fixed obligation upfront, fees, and early-exit execution affect the overall cost of the strategy.
- **Ongoing management:** Repaying or changing the loan does not mean you should leave the hedge unchanged. Review both positions together.

Reduced floating receipts can leave part of the borrowing cost unhedged. See [Risks & Trust Assumptions](../../security/risks-and-trust-assumptions.md).

## Further reading

- [Long Rate](../../rates-trading/editor.md)
- [Open Position](../../rates-trading/images-and-media.md)
- [Close Position](../../rates-trading/integrations.md)
- [Settlement Accrual](../../market-mechanics/vamm/settlement-accrual.md)
- [Fees](../../rates-trading/fee.md)
