# Trade Rates

Use Rates Exchange to express a view on the rates traded in its [supported markets](../get-started/supported-markets.md). A rates trade creates a position on Rates Exchange; it does not create a loan or lending deposit in the underlying protocol.

## How it works

A long pays fixed and receives floating. A short receives fixed and pays floating. Changes in the implied rate affect the position's exit value, while floating payments accrue over its holding period.

Read [Long vs Short](../rates-trading/editor.md) before choosing a direction.

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

Monitor the position's size, accrued payments, and remaining term. If you are short, also monitor collateral and health. An unchanged quoted rate does not mean your available collateral is unchanged.

To exit, review [Closing & Expiry](../rates-trading/integrations.md). Closing a position and withdrawing the resulting available funds are separate actions.

## Risks and limitations

Liquidity, execution prices, fees, and payment obligations affect the result. Short positions can be liquidated. A prepaid long still carries market, protocol, and payment-shortfall risk.

## Further reading

- [Market Specifications](../rates-trading/market-specifications.md)
- [Collateral, Health & Liquidation](../rates-trading/interactive-blocks.md)
- [Payments & PnL](../rates-trading/payments-and-pnl.md)
- [Fees](../rates-trading/fee.md)
