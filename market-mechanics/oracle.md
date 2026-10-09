# Oracle

Every market settles floating payments on the rate of its underlying lending market. The oracle brings that rate to the base blockchain.

## How the floating rate reaches a market

The oracle reads the underlying market's borrow index, such as Aave's USDC variable borrow index, and Rates Exchange's relayer writes it on-chain alongside the user actions it submits. The source market can be on a different chain from the Rates Exchange market; the oracle carries the rate across.

Index values are recorded in **12-second epochs**, the same clock used for settlement and vAMM time decay. Floating payments are calculated from the growth in the index between two epochs. See [Settlement](vamm/settlement-accrual.md).

## Safeguards

- **The index can only grow.** An update that would lower the index is rejected.
- **Growth is capped.** An update that implies a rate above the feed's maximum APR is rejected. The maximum varies from market to market. It sits well above normal rates and caps the damage a faulty or compromised update can do.
- **One value per epoch.** The first value recorded for an epoch is final and cannot be overwritten.
- **The traded price is not an oracle input.** The oracle drives floating payments only. Implied rates come from trading on the order book and vAMM, so an oracle fault cannot move the market price directly.

## When updates stop

Settling a position needs the oracle value for the current epoch. If updates stop, actions that settle accrued payments, including trades, collateral withdrawals, and liquidations, cannot execute until updates resume. No payments are lost: once updates resume, accrual covers the whole gap.

## Related mechanics

- [Settlement](vamm/settlement-accrual.md)
- [Implied Rate & Mark Rate](vamm/README.md)
- [Risks & Trust Assumptions](../security/risks-and-trust-assumptions.md)
