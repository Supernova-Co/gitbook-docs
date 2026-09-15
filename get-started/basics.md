# Rates Exchange Basics

A rate describes a cost or return over time. Rates Exchange lets you trade that rate exposure separately from the underlying loan or deposit.

## Fixed and floating

A floating rate changes with its underlying market. A fixed rate is agreed when a rates trade executes for the remaining term of that market.

| Position | Fixed side | Floating side |
| --- | --- | --- |
| Long | Pays fixed upfront | Receives floating |
| Short | Receives fixed upfront | Pays floating |

The upfront fixed payment is not the full principal of an underlying loan. It represents the fixed obligation for the position's notional and remaining term.

## Implied rate and underlying rate

The **implied rate** is the rate at which participants trade the remaining exposure. The **underlying rate** determines floating accrual.

These are different quantities. A change in the implied rate changes the value of an open position. Floating accrual changes the payments received or owed while that position remains open.

## Notional, funds, and expiry

- **Notional** describes the size of the rate exposure. It is not the amount deposited into your Rates Exchange account.
- **Collateral** backs the obligations of a short position. Funds committed to positions or orders are not necessarily available to withdraw.
- **Expiry** is the end of the rates market's term. The current beta markets expire monthly.

A monthly expiration schedule is not a promise that every new position lasts a full month. A position opened within an existing market has that market's remaining term.

## Trading and hedging

A trader may take a long or short to express a view on rates. A borrower can combine a long with a floating-rate loan; a lender can combine a short with floating-rate lending income.

The hedge and the underlying exposure remain separate. Differences in their size, benchmark, term, and costs can affect the result.

## Next steps

1. Check [Supported Markets](supported-markets.md).
2. Read [Fund & Withdraw](fund-and-withdraw.md).
3. Choose a product from the User Guides section.
4. Review [Risks & Trust Assumptions](../security/risks-and-trust-assumptions.md) before opening a position.
