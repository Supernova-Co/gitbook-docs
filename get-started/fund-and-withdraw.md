# Fund & Withdraw

Use [Rates Exchange](https://beta.rates.exchange) to manage the funds used for your rates positions.

## Your accounts

| Account | What it holds |
| --- | --- |
| Wallet | Your tokens outside Rates Exchange, used to fund your account and receive withdrawals. |
| Funding account | Deposited tokens available to move into an isolated account, cover gas top-ups, or withdraw. These funds do not back positions. |
| Isolated account | Funds allocated to a specific market. Only funds in this account back positions in that market. |

Funds in your wallet, funding account, or another market’s isolated account do not count toward a position’s collateral.

## Before you start

Your Rates Exchange position is separate from any loan or lending deposit you hold on Aave. Funding your Rates Exchange account does not create or repay an underlying loan, and withdrawing from it does not withdraw your underlying lending deposit.

Collateral must match the underlying loan token: **USDC for USDC borrow-rate markets, and USDT for USDT borrow-rate markets**.

Check the transfer network and destination in [Rates Exchange](https://beta.rates.exchange) before sending funds.

## Fund your account

{% stepper %}
{% step %}
### Open Rates Exchange

Go to [Rates Exchange](https://beta.rates.exchange) and access the account you intend to use for your rates positions.
{% endstep %}

{% step %}
### Deposit USDC or USDT

Deposit the token for your market into your Rates Exchange funding account: **USDC for USDC markets, or USDT for USDT markets**. Confirm the amount, transfer network, and destination before authorizing the deposit.
{% endstep %}

{% step %}
### Allow for gas and confirm your deposit

Swaps, deposits, and withdrawals typically cost **$0.01 per action**, paid from a separate gas balance in the same token. When it runs low, Rates Exchange can automatically top it up from your funding account and, if needed, your wallet.

After the deposit completes, confirm the funds appear in your funding account's available balance. Funds used for gas top-ups are kept separately from that balance. See [Gas balances](../rates-trading/fee.md#gas-balances).
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
### Withdraw available funds

Choose USDC or USDT and an amount within your available funding balance. Confirm the destination and transfer network, then authorize the withdrawal.

Withdrawal gas is paid from the gas balance for that token, typically about **$0.01 per action**. An automatic gas top-up may use funds from your funding account or wallet.
{% endstep %}

{% step %}
### Confirm the funds arrived

Once the transfer completes, confirm the USDC or USDT has arrived at the destination on the selected network. A decrease in your Rates Exchange balance alone does not confirm receipt.
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
