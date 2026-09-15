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

## An order's path

An order is evaluated against available order-book and vAMM liquidity. Execution may involve more than one venue. The resulting exposure and balance changes belong to the same rates market.

Order-book counterparties and the vault are different sources of liquidity. The vault does not need to be the counterparty to a trade matched entirely between users.

## Constraints matter

A pricing curve is not a guarantee that every trade size can execute. Available liquidity, collateral requirements, and market constraints affect execution. A quote, an accepted order, and a completed fill should be distinguished.

## Related mechanics

- [Orders & Execution](order-book.md)
- [Pricing & Mark Rates](vamm/README.md)
- [Collateral Accounting](position-health.md)
- [Settlement](vamm/settlement-accrual.md)
- [Vault Mechanics](vault/README.md)

<a id="market-liquidity"></a>
<a id="vault--vamm-counterparty"></a>
<a id="mm--order-book-limit-orders"></a>
<a id="why-both-are-needed"></a>
<a id="flow-routing"></a>
