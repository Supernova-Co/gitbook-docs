# Rates Exchange Basics

A rate describes a cost or return over time. Rates Exchange lets you trade that rate exposure separately from the underlying loan or deposit.

## Fixed and floating

Each rates position has two sides:

- **Fixed side: implied rate.** The implied rate at execution sets your fixed obligation for the remaining term. The market's implied rate can change afterward, affecting your position's value, but your agreed fixed obligation stays the same.
- **Floating side: underlying rate.** The underlying rate changes with the lending market and determines the floating payments that accrue while your position is open.

| Position | Fixed side (implied rate at execution) | Floating side (underlying rate) |
| --- | --- | --- |
| Long | Pays fixed upfront | Receives floating |
| Short | Receives fixed upfront | Pays floating |

The upfront fixed payment is not the full principal of an underlying loan. It represents the fixed obligation for the position's notional and remaining term.

## Notional, funds, and expiry

- **Notional** describes the size of the rate exposure. It is not the amount deposited into your Rates Exchange account.
- **Collateral** backs the obligations of a short position. Funds committed to positions or orders are not necessarily available to withdraw.
- **Expiry** is the end of the rates market's term. Current markets expire monthly.

A monthly expiration schedule is not a promise that every new position lasts a full month. A position opened within an existing market has that market's remaining term.

## Next steps

1. Check [Supported Markets](supported-markets.md).
2. Read [Fund & Withdraw](fund-and-withdraw.md).
3. Choose a product from the User Guides section.
4. Review [Risks & Trust Assumptions](../security/risks-and-trust-assumptions.md) before opening a position.
