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
