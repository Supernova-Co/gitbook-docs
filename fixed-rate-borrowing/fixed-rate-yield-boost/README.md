# Lend with Yield Boost

<a id="yield-boost"></a>

<a id="why-lenders-like-it"></a>

<a id="what-is-yield-boost"></a>

## What it does

Yield Boost combines lending on Aave with a separate short rates position on Rates Exchange. It is designed to improve your yield by supporting fixed-rate borrowing while your lending capital stays in Aave earning variable yield. The combined strategy also aims to make your returns more predictable.

Use the **Yield Boost page on Rates Exchange** to access this strategy.

<a id="how-the-economics-work"></a>

## How it works

You hold two separate positions:

| Position | Where it lives | What it does |
| --- | --- | --- |
| Lending deposit | Aave | Earns variable lending yield |
| Short rates position | Rates Exchange | Receives a fixed payment upfront and pays the floating borrow rate over the chosen term |

Your lending capital stays in Aave. The short requires separate collateral on Rates Exchange.

Rates Exchange’s interest-rate markets track borrow rates, while your deposit earns a lending rate. Because those rates differ, the short’s size matters. Use the Yield Boost page to review the strategy, including its hedge size, term, and collateral requirements.

## How to use it

{% stepper %}
{% step %}
### Open the Yield Boost page

Connect your wallet and open **Yield Boost** on Rates Exchange.
{% endstep %}

{% step %}
### Choose your lending market

Use a supported Aave lending market. Your deposit continues earning variable lending yield and remains subject to Aave’s withdrawal rules.
{% endstep %}

{% step %}
### Review the strategy

Check the short position’s notional, fixed rate, term, required collateral, and fees. Consider these alongside your Aave lending deposit.
{% endstep %}

{% step %}
### Fund and open the short

Provide the required collateral on Rates Exchange and confirm the trading authorization and transaction prompts shown in the app.

The short receives fixed and pays floating. Keep track of both the Aave deposit and the Rates Exchange position.
{% endstep %}
{% endstepper %}

## Managing the position

### Collateral

The short requires its own collateral on Rates Exchange. Monitor its health and add collateral or reduce exposure when needed. Your Aave deposit does not automatically back the short.

<a id="withdrawing-the-underlying-deposit"></a>

### Withdrawing your Aave deposit

Withdrawals remain subject to Aave’s liquidity and rules. Withdrawing your deposit does not close the Rates Exchange short or stop its floating-payment obligations.

Review the hedge whenever you reduce or withdraw the deposit.

<a id="closing-the-hedge"></a>

### Closing the short

Closing the short ends the hedge. If you keep your Aave deposit, it continues earning variable lending yield.

Your closing outcome depends on the available execution rate and applicable fees. See [Closing & Expiry](../../rates-trading/payments-and-pnl.md#close-position) before exiting.

### Expiry

The short settles at the end of its chosen term. Your Aave lending deposit remains separate and continues under Aave’s rules.

**Auto-roll is upcoming and is not currently available.**

## Risks and limitations

- **Underlying protocol risk:** Your deposit remains exposed to Aave’s risks and withdrawal conditions.
- **Liquidation risk:** The short can be liquidated if its collateral becomes insufficient.
- **Rate differences:** Your deposit earns the lending rate, while the short pays the borrow rate. These payments may not offset exactly.
- **Execution and fees:** Entry and exit rates, available liquidity, and fees affect your combined return.
- **Separate positions:** Changes to your Aave deposit do not automatically adjust or close your Rates Exchange short.

## Further reading

- [Fund & Withdraw](../../get-started/fund-and-withdraw.md)
- [Short Rate](../../rates-trading/markdown.md)
- [Closing & Expiry](../../rates-trading/payments-and-pnl.md#close-position)
- [Position Health](../../market-mechanics/position-health.md)
- [Liquidation & Loss Allocation](../../market-mechanics/liquidation.md)
- [Fees](../../rates-trading/fee.md)
