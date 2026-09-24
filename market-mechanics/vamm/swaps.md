# Swaps

A swap exchanges fixed and floating rate exposure for a market's remaining term. A long pays fixed and receives floating; a short receives fixed and pays floating.

## Constant-product pricing

<a id="constant-product-pricing"></a>

The vAMM quotes using a constant-product relationship between virtual reserves. A trade changes the reserve ratio, so the marginal quote after execution can differ from the quote before it.

Price impact depends on trade size and virtual curve depth.

## Time decay

<a id="deterministic-decay"></a>

As expiry approaches, the fixed obligation represented by the remaining term becomes smaller at an unchanged implied rate. Time decay and a change in the market's annualized rate are different effects.

## Execution and costs

Routing can combine order-book and vAMM fills at different rates. The filled sizes and execution rates determine the position’s entry value; trading fees are charged separately.

See [Implied Rate & Mark Rate](README.md), [Orders & Execution](../order-book.md), and [Fees](../../rates-trading/fee.md).
