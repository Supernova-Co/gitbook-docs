---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Overview

Rates Exchange is an exchange for trading and hedging rates. Its private beta is live at [beta.rates.exchange](https://beta.rates.exchange), with monthly-expiring markets for Aave USDC and USDT borrow rates on Ethereum mainnet.

## Choose your starting point

| Your goal | Where to start |
| --- | --- |
| Make borrowing costs more predictable | [Borrow at a Fixed Rate](fixed-rate-borrowing/user-guide-one-click-fixing-rate/borrow-at-fixed-rate-from-aave-morpho.md) |
| Hedge floating lending income | [Lend with Yield Boost](fixed-rate-borrowing/fixed-rate-yield-boost/README.md) |
| Express a view on rates | [Trade Rates](user-guides/trade-rates.md) |
| Understand vault participation | [Provide Vault Liquidity](user-guides/provide-vault-liquidity.md) |

## What changes hands?

A rates position exchanges a fixed obligation for payments linked to an underlying floating rate. It does not require exchanging the full principal represented by the position's notional.

A long pays fixed and receives floating. A short receives fixed and pays floating. Both refer to the same market and expiry, but they have different funding requirements and risks.

For borrowers and lenders, the rates position is separate from the loan or deposit in the underlying lending protocol. For traders, the position provides rate exposure without creating that underlying loan or deposit.

## How execution works

An order book matches orders, while a virtual automated market maker, or vAMM, provides another execution venue. The vault is the counterparty to trades executed through the vAMM. Availability and execution depend on market liquidity and applicable constraints.

Start with [Rates Exchange Basics](get-started/basics.md), check [Supported Markets](get-started/supported-markets.md), or read our [Mission](README.md).
