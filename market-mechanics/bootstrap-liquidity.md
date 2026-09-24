# Architecture & Routing

Rates Exchange separates the account holding funds, the execution venues, the market positions, and floating-rate settlement.

## Components

| Component | Responsibility |
| --- | --- |
| Account and clearing | Records available funds and funds assigned to market positions |
| Router | Coordinates execution across available venues |
| Order book | Matches orders with resting liquidity |
| vAMM | Quotes through a virtual pricing curve |
| Vault | Acts as counterparty to vAMM flow and participates in market loss absorption |
| Rate data and settlement | Supplies the underlying-rate information used to account for floating payments |

## Order routing

Orders route to the order book, the vAMM, or both, depending on available liquidity. Fills update the trader’s position and balance within the same rates market.

- **Order-book fills:** Match against resting user orders.
- **vAMM fills:** Execute against the virtual pricing curve, with the vault taking the opposite exposure.

## vAMM pricing

The vAMM uses a constant-product curve of virtual reserves:

```text
k = baseReserve × quoteReserve
Price = baseReserve / quoteReserve
```

Trades change the reserve ratio and marginal quote. Price impact depends on trade size and virtual curve depth.

At an unchanged implied APR, the fixed payment for the remaining term decreases as expiry approaches:

```text
Price = Implied APR × Remaining duration in days / 365
```

Between trades, `decayFixed` adjusts the reserves while preserving the constant product and implied APR. At expiry, the remaining-term value reaches zero. This time decay changes the fixed-payment value without changing the annualized rate.

See [Implied Rate & Mark Rate](vamm/README.md) for APR conversion and risk valuation.

## Related mechanics

- [Orders & Execution](order-book.md)
- [Implied Rate & Mark Rate](vamm/README.md)
- [Collateral Accounting](position-health.md)
- [Settlement](vamm/settlement-accrual.md)
- [Vault Mechanics](vault/README.md)

<a id="market-liquidity"></a>
<a id="vault--vamm-counterparty"></a>
<a id="mm--order-book-limit-orders"></a>
<a id="why-both-are-needed"></a>
<a id="flow-routing"></a>
