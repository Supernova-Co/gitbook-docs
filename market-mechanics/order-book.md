# Orders & Execution

Rates Exchange orders express a desired rate exposure in a market with a specific expiry.

## Market and limit orders

| Order | Purpose | Important distinction |
| --- | --- | --- |
| Market | Seek execution against available liquidity | The resulting execution depends on available rates and size |
| Limit | Specify a rate or better | An order can remain unfilled |

Execution can use order-book or vAMM liquidity. Do not assume that placing a limit order means it must execute solely against another resting order.

## Order lifecycle

A resting order is different from an open position. Check whether an order is active, filled, partially filled, or cancelled before deciding what exposure remains.

Limit orders are described as good until cancelled. At market expiry, the order book closes and remaining open orders are cancelled.

## Funds reserved for orders

Orders can reserve funds or existing exposure so that execution is backed. Reserved amounts are not freely reusable for another order, position, or withdrawal.

An order's continued executability depends on the account's ability to support the resulting trade. An apparent order-book level should not be treated as an unconditional promise of execution.

## Cancelling and closing

Cancelling an unfilled order removes an execution instruction. Closing an existing position trades out of exposure. These are different actions, and cancelling an order does not erase exposure from earlier fills.

See [Trade Rates](../user-guides/trade-rates.md), [Open Position](../rates-trading/images-and-media.md), and [Collateral Accounting](position-health.md).

<a id="order-book"></a>
