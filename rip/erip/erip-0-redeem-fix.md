# ERIP-0: Redeem Fix

Committed: November 19, 2022

---

- [Submitter](#submitter)
- [Emergency Process Note](#emergency-process-note)
- [Links](#links)
- [Problem](#problem)
- [Solution](#solution)
- [Contract Changes](#contract-changes)
- [Effective](#effective)

## Submitter

Root DAO Multisig (RDM)

## Emergency Process Note

Per the process outlined in the [RDM Emergency Response Procedures](https://docs.roottoken.org/governance/root-token/rdm-process#emergency-response-procedures), the RDM can take swift action to protect Root in the event of a bug or security vulnerability.

This bug was reported by a whitehat on Immunefi.

## Links

- [GitHub Commit Hash](https://github.com/BeanstalkFarms/Beanstalk/pull/151)
- [Gnosis Transaction](https://app.safe.global/eth:0xb7774ec5031e1d903152E96BbC1601e5D0D83Ca2/transactions/tx?id=multisig_0xb7774ec5031e1d903152E96BbC1601e5D0D83Ca2_0x9fcf0758777f5f57c0719bfb685fa6d8f4c8b2344f8a1acf23e85057c849352b)
- [Etherscan Transaction](https://etherscan.io/tx/0xf9b52baec84555347dac1ae6b3354bb77947c3f62ef76fcb87e47c58429e7576)
- [Arweave](https://arweave.net/7fjU88EiBrvbLK8oW_GRld4DsSxYfm0yLVvm0x7ywnM)

## Problem

According to Section 3.3 of the [Root whitepaper](https://roottoken.org/root.pdf#subsection.3.3), the amount of Roots to be Redeemed from a set of Deposits  is derived from the maximum percentage change in the BDV, Stalk and Seeds of Root as a result of the Redemption.

However, in the Root code, the Roots to Redeem used the mininum instead of the maximum which allowed the user to receive more Bean Deposits than they were supposed to when Redeeming. 

In total it is estimated that an additional ~226 Beans were Redeemed across 12 transactions.

## Solution

Update the `_transferDeposits()` function to subtract the minimum amount remaining from the supply in accordance with Section 3.3 of the [Root whitepaper](https://roottoken.org/root.pdf#subsection.3.3). Because subtraction occurs in the `_transferDeposits()` function, subtracting the maximum amount remaining from the supply resulted in the minimum of the change in BDV, Stalk and Seeds per Root required to Redeem being used instead of the maximum.

The fix has been sent to Halborn.

## Contract Changes

The following callable functions are modified in Root:

|     Name      |   Selector   |
|:--------------|:-------------|
| `redeem(...)` | `0x048f0869` |

## Effective

Effective immediately upon commit by the RDM, which has already happened.
