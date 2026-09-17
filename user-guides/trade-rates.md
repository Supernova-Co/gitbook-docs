# Trade Rates

Use Rates Exchange to express a view on the rates traded in its [supported markets](../get-started/supported-markets.md). A rates trade creates a position on Rates Exchange; it does not create a loan or lending deposit in the underlying protocol.

## How it works

A long pays its full fixed obligation upfront and receives floating payments over the chosen term. **A long rates position cannot be liquidated because its fixed payment is already fully paid.** The floating payments it receives continue to accrue over time; they are not settled upfront.

A short receives fixed upfront and pays floating over time. It must maintain sufficient collateral and can be liquidated if that collateral falls below the market's maintenance requirement.

A rise in the implied rate generally improves a long's exit value and worsens a short's. A fall generally has the opposite effect. Floating payments, the remaining term, and fees also affect the position's total PnL.

## How to use it

{% stepper %}
{% step %}
### Access and fund your account

Open [Rates Exchange](https://beta.rates.exchange). Follow [Fund & Withdraw](../get-started/fund-and-withdraw.md) and confirm your funds are available.
{% endstep %}
{% step %}
### Review the market

Check the underlying rate, expiry, quoted rate, and intended notional. Review the remaining term rather than assuming a newly opened position has a full month to run.
{% endstep %}
{% step %}
### Choose a direction and execution method

Choose long or short according to the exposure you intend to take. A market order seeks available execution; a limit order specifies a rate or better and may remain unfilled.

Check the required funds and applicable costs before submitting the order. See [Orders & Execution](../market-mechanics/order-book.md).
{% endstep %}
{% step %}
### Confirm the resulting position

Check whether the order filled and review the resulting position. An open order and an open position are different: an order can remain outstanding while an existing position continues to accrue payments.
{% endstep %}
{% endstepper %}

## Managing the position

Monitor the position's size, accrued payments, and remaining term. If you are short, also monitor collateral and health. Floating payments are deducted from your short position's collateral over time, even when the market's quoted fixed rate stays the same.

To exit, review [Closing & Expiry](../rates-trading/payments-and-pnl.md#close-position). Closing a position and withdrawing the resulting available funds are separate actions.

## Risks and limitations

Liquidity, execution prices, fees, and payment obligations affect the result. Short positions can be liquidated. A prepaid long still carries market, protocol, and payment-shortfall risk.

## Further reading

- [Supported Markets](../get-started/supported-markets.md)
- [Managing Collateral](../rates-trading/interactive-blocks.md)
- [Payments, PnL & Expiry](../rates-trading/payments-and-pnl.md)
- [Fees](../rates-trading/fee.md)
