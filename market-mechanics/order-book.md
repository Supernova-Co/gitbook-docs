# Orders & Execution

Rates Exchange orders express a desired rate exposure in a market with a specific expiry.

## Market and limit orders

| Order | Purpose | Important distinction |
| --- | --- | --- |
| Market | Seek execution against available liquidity | The resulting execution depends on available rates and size |
| Limit | Specify a rate or better | An order can remain unfilled |

## Order lifecycle

A resting order is different from an open position. Check whether an order is active, filled, partially filled, or cancelled before deciding what exposure remains.

Limit orders are described as good until cancelled. At market expiry, the order book closes and remaining open orders are cancelled.

## Collateral for orders and positions

Orders and positions use funds in the relevant isolated market account. Funds in your wallet, funding account, or another market’s account do not back them.

**Reserved collateral cannot be reused.** Funds locked for an open order cannot also back another order or position. Remaining available collateral can support additional trades, subject to health checks.

### Closing a position

- **Closing a long:** Place a sell order. It reserves the portion of your long being closed, with no additional collateral required. That reserved portion cannot be used for another order or close.
- **Closing a short:** Place a buy order. It reserves the full payment needed to buy back the short. Add funds only if your available balance cannot cover that payment.

### Partial fills and cancellations

A partial fill does not release the order’s reservation. The reservation remains until the order fills completely or is cancelled. Cancel and replace the remaining order to recalculate its requirement.

Cancelling an order releases its reservation but does not close any position created by earlier fills.

### Withdrawals

- **Open orders:** Cancel open orders before withdrawing. Withdrawals are blocked while orders remain open.
- **Open positions:** An open position does not lock your entire balance. You can withdraw available collateral if the remaining collateral passes the required health checks.

### Checks at execution

Collateral is checked again when an order is about to fill. If it no longer supports the trade, the fill is blocked and the order is removed.

See [Trade Rates](../user-guides/trade-rates.md), [Open Position](../rates-trading/images-and-media.md), and [Collateral Accounting](position-health.md).

<a id="order-book"></a>
