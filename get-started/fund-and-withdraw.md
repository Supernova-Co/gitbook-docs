# Fund & Withdraw

Use [beta.rates.exchange](https://beta.rates.exchange) to access the Rates Exchange private beta and manage the funds used for your rates positions.

## Before you start

Your Rates Exchange position is separate from any loan or lending deposit you hold on Aave. Funding your Rates Exchange account does not create or repay an underlying loan, and withdrawing from it does not withdraw your underlying lending deposit.

The network listed on [Supported Markets](supported-markets.md) identifies the underlying borrow-rate market. Check the funding instructions in the beta for the assets and networks accepted for transfers.

## Fund your account

{% stepper %}
{% step %}
### Open the private beta

Go to [beta.rates.exchange](https://beta.rates.exchange) and access the account you intend to use for your rates positions.
{% endstep %}

{% step %}
### Review the funding instructions

Follow the funding instructions provided in the beta. Check the transfer asset, network, destination, and amount before authorizing a transfer, along with any applicable transaction costs.
{% endstep %}

{% step %}
### Check your balance before opening a position

Confirm that the funding has completed and the funds are available in your Rates Exchange account before opening a position.

A long rate position pays its fixed obligation upfront. A short rate position requires collateral to support its floating-payment obligations. Review the requirements for the position you intend to open.
{% endstep %}
{% endstepper %}

## Withdraw funds

{% stepper %}
{% step %}
### Review your positions and orders

Check whether funds are committed to open positions or resting orders. Your total balance should not be assumed to be fully available for withdrawal.

Removing collateral from an open short must leave the position within its required health limits. See [Position Health](../market-mechanics/position-health.md).
{% endstep %}

{% step %}
### Review the withdrawal instructions

Follow the withdrawal instructions provided in the beta. Check the available amount, destination, transfer asset, network, and any applicable costs before authorizing the withdrawal.
{% endstep %}

{% step %}
### Confirm receipt

Check that the withdrawal has completed and the funds have arrived at the intended destination. A submitted request should not be treated as a completed transfer.
{% endstep %}
{% endstepper %}

## Managing an underlying loan or deposit

Use the underlying lending protocol's process to repay a loan or withdraw a lending deposit. Review your Rates Exchange hedge whenever that underlying exposure changes.

Closing a hedge and withdrawing funds are separate actions. Closing a Rates Exchange position does not itself repay your Aave loan or withdraw your lending deposit.

## Need help?

Email [team@rates.exchange](mailto:team@rates.exchange) for help with funding or withdrawals.

## Further reading

- [Borrow at a Fixed Rate](../fixed-rate-borrowing/user-guide-one-click-fixing-rate/borrow-at-fixed-rate-from-aave-morpho.md)
- [Lend with Yield Boost](../fixed-rate-borrowing/fixed-rate-yield-boost/README.md)
- [Close Position](../rates-trading/integrations.md)
- [Position Health](../market-mechanics/position-health.md)
- [Fees](../rates-trading/fee.md)
