# Swaps

A swap exchanges fixed and floating rate exposure for a market's remaining term. A long pays fixed and receives floating; a short receives fixed and pays floating.

## Constant-product pricing

<a id="constant-product-pricing"></a>

The vAMM quotes using a constant-product relationship between virtual reserves. A trade changes the reserve ratio, so the marginal quote after execution can differ from the quote before it.

Price impact depends on trade size and virtual curve depth.

## Time decay

<a id="deterministic-decay"></a>

At an unchanged implied APR, the fixed payment for the remaining term decreases as expiry approaches:

```text
Price = Implied APR × Remaining duration in days / 365
```

Between trades, `decayFixed` adjusts the virtual reserves while preserving the constant product and implied APR. At expiry, the remaining-term value reaches zero.

Time decay changes the remaining fixed-payment value without changing the annualized rate.

## Execution and costs

Routing can combine order-book and vAMM fills at different rates. The filled sizes and execution rates determine the position’s entry value; trading fees are charged separately.

See [Implied Rate & Mark Rate](README.md), [Orders & Execution](../order-book.md), and [Fees](../../rates-trading/fee.md).
