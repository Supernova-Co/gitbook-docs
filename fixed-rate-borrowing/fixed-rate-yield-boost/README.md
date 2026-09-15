# Lend with Yield Boost

<a id="yield-boost"></a>

<a id="why-lenders-like-it"></a>

<a id="what-is-yield-boost"></a>

## What it does

Yield Boost combines lending on Aave with a separate rates position on Rates Exchange. It is designed to make lending returns more predictable and may improve yield when market conditions are favorable.

A higher return is not guaranteed.

<a id="how-the-economics-work"></a>

## How it works

You manage two separate positions:

| Position | Where it lives | What it does |
| --- | --- | --- |
| Lending deposit | Aave | Earns the underlying protocol’s floating lending yield |
| Short rate position | Rates Exchange | Receives the fixed payment upfront and pays floating over the chosen term |

The short position is the hedge. It requires additional collateral on Rates Exchange; your underlying lending deposit remains in Aave.

The two positions are intended to offset some floating-rate exposure. Their payments should not be assumed to cancel exactly. Your combined return depends on both positions and their costs, rather than simply adding the quoted fixed rate to your lending yield.

## How to use it

{% stepper %}
{% step %}
### Start with a lending deposit

Lend through a supported Aave market. Your deposit continues to earn that market’s floating lending yield and remains subject to its rules and risks.
{% endstep %}

{% step %}
### Review the market and term

Review the available rates market, its quoted fixed rate, and its term, also called its tenor.

A quoted fixed rate above your current lending rate does not by itself establish the return you will earn. Consider the floating payments owed by the hedge and the costs of the position.
{% endstep %}

{% step %}
### Choose how to enter

A market order seeks execution at the available market rate. A limit order specifies your target rate or better and may remain unfilled.

Rates Exchange can route execution through the order book or vAMM.
{% endstep %}

{% step %}
### Open the short rate position

Provide the required collateral for the Rates Exchange position and enter the short: receive fixed and pay floating.

Keep track of both the underlying lending deposit and the separate rates position.
{% endstep %}
{% endstepper %}

## Managing the position

### Collateral

The Rates Exchange short requires its own collateral. Keeping your lending deposit in Aave does not remove the obligations or risks of that separate position.

### Withdrawing the underlying deposit

Withdrawals remain subject to the underlying protocol’s liquidity and rules. Treat withdrawing the deposit and closing the hedge as separate actions.

Do not assume that withdrawing your deposit also closes the Rates Exchange short or removes its floating-payment obligations.

### Closing the hedge

Closing the Rates Exchange short ends the hedge. If you retain your underlying deposit, it continues to earn floating lending yield.

The outcome of closing depends on the position’s exit terms and execution. Review the existing closing explanation before exiting.

### Expiry

The rates position has a chosen term, while the underlying lending deposit is separate. Plan for that term to end. **Auto-roll is upcoming and is not currently available.**

## Risks and limitations

- **Underlying protocol risk:** Your deposit remains exposed to the risks and withdrawal conditions of Aave.
- **Additional hedge risk:** The Rates Exchange position introduces separate collateral commitments and payment obligations.
- **Imperfect offset:** Floating income from the deposit and floating payments on the hedge may differ.
- **Return uncertainty:** A quoted rate or spread is not a guaranteed yield premium. Costs and the performance of both positions affect the result.
- **Execution and exit:** A limit order may not fill. Do not assume entry or closure is always available at your desired rate.
- **Separate management:** Changes to your lending deposit should prompt a review of the hedge that accompanies it.

A short hedge can be liquidated if its collateral becomes insufficient. This ends or reduces the intended hedge and does not remove the risks of the underlying deposit. See [Risks & Trust Assumptions](../../security/risks-and-trust-assumptions.md).

## Further reading

- [Short Rate](../../rates-trading/markdown.md)
- [Order Book](../../market-mechanics/order-book.md)
- [Close Position](../../rates-trading/integrations.md)
- [Position Health](../../market-mechanics/position-health.md)
- [Liquidation](../../market-mechanics/liquidation.md)
- [Settlement Accrual](../../market-mechanics/vamm/settlement-accrual.md)
- [Fees](../../rates-trading/fee.md)
