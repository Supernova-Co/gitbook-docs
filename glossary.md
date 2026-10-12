# Glossary

## Underlying rate

The rate source used to calculate a market's floating accrual. Current markets cover Aave USDC and USDT borrow rates on Ethereum mainnet; a complete market identity also needs its source market and expiry.

## Implied rate

The annualized rate expressed through trading. It describes the remaining rate exposure and is distinct from the realized underlying floating rate.

## Notional

The size of the rate exposure, not the amount deposited. See [Rates Exchange Basics](get-started/basics.md#notional-funds-and-expiry).

## Expiry and remaining term

Expiry is the end of a market's term; remaining term is the time left until it.  Monthly expiration does not mean a position opened mid-term lasts a full month. See [Rates Exchange Basics](get-started/basics.md#notional-funds-and-expiry).

## Long rate

A position that pays fixed and receives floating. See [Rates Exchange Basics](get-started/basics.md#fixed-and-floating).

## Short rate

A position that receives fixed and pays floating. See [Rates Exchange Basics](get-started/basics.md#fixed-and-floating).

## Fixed payment

The fixed side for the market's remaining term, exchanged at entry. See [Rates Exchange Basics](get-started/basics.md#fixed-and-floating).

## Collateral

Funds backing a position's obligations. Available account balance, position collateral, and funds reserved for orders should be distinguished.

## Mark and execution price

A mark is used for valuation or risk checks under the market's rules. An execution price is the price at which a trade actually fills. They need not be equal.

## Accrual and settlement

Accrual measures the amount earned or owed over time. Settlement accounts for obligations in balances. Neither term should be assumed to mean a transfer to an external wallet.

## PnL

Profit and loss. A complete rates-position result considers fixed payments, floating accrual, closing value, and costs. A hedged strategy also includes the underlying loan or deposit.

## Vault shares

A proportional interest in a vault. Share value reflects the vault's accounting for assets, obligations, income, and losses; it is not a guarantee of deposited principal.

## Health

A measure of whether a position has sufficient backing under its market's rules. Opening requirements and liquidation conditions are different checks.

## Further reading

- [Rates Exchange Basics](get-started/basics.md)
- [Supported Markets](get-started/supported-markets.md)
- [Collateral Accounting](market-mechanics/position-health.md)
