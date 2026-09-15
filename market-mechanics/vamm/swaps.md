# Swaps

A swap exchanges fixed and floating rate exposure for a market's remaining term. A long pays fixed and receives floating; a short receives fixed and pays floating.

## Constant-product pricing

<a id="constant-product-pricing"></a>

The vAMM quotes using a constant-product relationship between virtual reserves. A trade changes the reserve ratio, so the marginal quote after execution can differ from the quote before it.

The price impact depends on the trade and the available curve depth. Virtual reserve quantities do not represent a user's deposited collateral.

## Time decay

<a id="deterministic-decay"></a>

As expiry approaches, the fixed obligation represented by the remaining term becomes smaller at an unchanged implied rate. Time decay and a change in the market's annualized rate are different effects.

## Execution and costs

Routing can combine order-book and vAMM liquidity. Review the executed size and rate, applicable costs, and resulting position rather than assuming the initial quote describes every fill.

See [Pricing & Mark Rates](README.md), [Orders & Execution](../order-book.md), and [Fees](../../rates-trading/fee.md).
