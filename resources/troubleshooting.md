# Troubleshooting & Support

Start by identifying whether the issue concerns your Rates Exchange account, an order, a position, or an underlying lending protocol.

## Funding has not appeared

Check the transfer status, destination, asset, and network against the funding instructions you used. Distinguish a submitted transfer from a completed transfer and an available account balance.

See [Fund & Withdraw](../get-started/fund-and-withdraw.md).

## An order has not filled

Check whether it is a limit order waiting for an executable rate, whether any part has filled, and whether the order is still active. A submitted order is not the same as an open position.

See [Orders & Execution](../market-mechanics/order-book.md).

## Funds are not available to withdraw

Review open positions and orders that may commit funds. Check whether the balance belongs to your trading account, a rates position, a vault, or an underlying lending deposit. These are different withdrawal contexts.

See [Managing Collateral](../rates-trading/interactive-blocks.md) and [Vault Mechanics](../market-mechanics/vault/README.md).

## Position health changed without a large rate move

A short owes floating payments over time. Accrual can reduce its collateral even if the implied rate has not moved sharply.

Review both the price used for health checks and the payments accrued by the position.

## The result differs from the quoted rate

A quoted annualized rate is not a complete statement of cash profit. Review the notional, remaining term, floating payments, closing value, and costs. For a hedge, include the underlying loan or deposit.

See [PnL](../rates-trading/payments-and-pnl.md).

## The underlying loan or deposit changed

Repaying a loan or withdrawing a lending deposit does not mean the separate rates hedge has closed. Review the hedge after changes to the underlying exposure.

## Contact support

For help with Rates Exchange, email [team@rates.exchange](mailto:team@rates.exchange).

## Information to collect for a support request

Record the affected market, approximate time, order or transaction reference, and the error message or unexpected result. Never include a seed phrase, private key, or password.
