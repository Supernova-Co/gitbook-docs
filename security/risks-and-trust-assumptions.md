# Risks & Trust Assumptions

Rates Exchange positions depend on market execution, collateral, settlement, and the protocols supplying the underlying rates. A hedge changes an exposure; it does not remove every source of risk.

## Risks by activity

| Activity | What to understand |
| --- | --- |
| Borrowing with a rates hedge | The underlying loan can still be liquidated. A hedge can differ from the loan in benchmark, size, term, or payment outcome. |
| Lending with Yield Boost | The underlying deposit and the short position have separate risks. The short requires collateral and can be liquidated. |
| Trading rates | Changes in implied rates, floating accrual, fees, and exit prices affect the result. |
| Providing vault liquidity | Vault shares can lose value through market exposure and losses the vault absorbs. Redemption can be constrained. |

## Liquidation and payment shortfalls

Short positions can become liquidatable when collateral no longer meets the required health conditions. A long's prepaid fixed obligation does not eliminate the possibility of losses, reduced receipts, or interruption of the intended hedge.

Losses may affect vault participants and the payments available to other market participants. Read [Liquidation & Loss Allocation](../market-mechanics/liquidation.md) alongside the guide for your product.

## Execution and withdrawal risk

An order may not fill at the desired rate or size. Closing a position depends on execution conditions. Funds backing positions or orders should not be treated as freely withdrawable.

Vault guardrails are constraints on activity, not a guarantee of a minimum share price or continuous access to liquidity.

## Underlying rates and protocol dependencies

Floating settlement depends on the rate information used by each market. The source protocol and the process that supplies its rate are part of the strategy's dependencies.

Smart contract failures and failures in connected services can affect funds or the ability to act. Keep the risks of an underlying lending protocol separate from those introduced by Rates Exchange.

## Audits

Audits provide evidence about a reviewed scope and version. They do not guarantee that every deployed component or future change is free of defects. See [Audits](audits.md).

## Security contact

To report a suspected vulnerability or security concern, email [security@rates.exchange](mailto:security@rates.exchange).
