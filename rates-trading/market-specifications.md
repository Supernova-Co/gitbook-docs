# Market Specifications

A Rates Exchange market is defined by an underlying rate and an expiry. Use both when identifying the exposure you intend to trade.

## Current markets

| Property | Description |
| --- | --- |
| Underlying protocol | Aave |
| Underlying rates | USDC and USDT borrow rates |
| Underlying network | Ethereum mainnet |
| Expiration schedule | Last Friday of the month at 15:00 UTC |
| Market opens | Approximately two weeks before the expiration month begins |
| Trading interface | [Rates Exchange](https://beta.rates.exchange) |

The underlying network identifies the source market. It does not by itself identify the network or asset accepted for account funding.

## Reading a rates position

| Term | Meaning |
| --- | --- |
| Notional | Size of the underlying rate exposure |
| Implied rate | Annualized rate agreed through trading |
| Remaining term | Time from the trade to the market's expiry |
| Long | Pays fixed upfront and receives floating |
| Short | Receives fixed upfront and pays floating, backed by collateral |
| Floating accrual | Payments determined from the market's underlying rate over time |

A quoted annualized rate and the cash required for a trade are not the same number. The remaining term and notional matter, as do fees and the position's funding requirements.

## Before placing an order

Check the exact underlying market, expiration date, position size, funds required, and quoted execution terms. Do not treat all USDC markets, or all USDT markets, as interchangeable.

See [Supported Markets](../get-started/supported-markets.md) to request an additional market, and [Orders & Execution](../market-mechanics/order-book.md) for order behavior.
