---
order: 1000
description: An overview of minting philosophy at Art Blocks.
---

# Minting Philosophy

An overview of the generative art minting philosophy at Art Blocks.

## Introduction

At Art Blocks, minting is a particularly special occasion where a new generative art piece is created. It is the final step in the generative art creation process, and enables collectors to partner with artists to create a unique, one-of-a-kind piece of generative art!

On a blockchain, "minting" is the process of creating new tokens. So not only is minting the process of creating new generative art pieces, it is also the process of creating new tokens on a blockchain. Typically, minting is also the point where a collector will pay for the generative art piece.

A few key points about minting at Art Blocks:

- Minting is the process of creating new generative art pieces.
- Minting is the process of creating new tokens on a blockchain.
- Minting generally involves a collector paying for the right to create a generative art piece.

## Core Principles

At Art Blocks, we are committed to providing a transparent minting toolkit for artists, and a transparent minting experience for collectors.

The following principles, when used together, are important ideals that we believe enable artists to achieve some sort of ["fairness"](#fairness) during their drop. They also are key to collector safety when interacting on a blockchain.

#### 1. Transparency

We believe that minting should be transparent and easy to understand for collectors. Verified source code is provided for all minter smart contracts, and we develop our minters publically in our open source [GitHub repository](https://github.com/ArtBlocks/artblocks-contracts).

#### 2. Decentralized & Trust-Minimized

We believe that minting should rely heavily on immutable smart contract code deployed to decentralized networks, and should be as trustless as possible. We aim to minimize the amount of trust in any centralized party when minting. This is important because collectors must feel safe when purchasing high-value generative art pieces, and trusting a centralized party to mint a generative art piece is often not an acceptable option.

Of course Artists and Art Blocks will have some elevated privileges, such as configuring auctions, but we aim to minimize those privileges and implement only when necessary. Those privileges will be documented and transparent, and should align incentives.

#### 3. Non-Custodial

Minting should be a transaction between the collector and the minter smart contract, and the contract should handle logic related to settlements, price changes over time, etc.

The minter smart contract should empower the collector to make their own decisions, and should not be custodial in nature.

#### 4. Honest

Blockchains have a unique set of technical quirks that can be exploited by opportunistic or malicious actors. These result in frequent discussions about bots, "flipping", and front-running.

We are committed to providing solutions to help alleviate these issues, but we are also committed to being honest about their limitations. Solutions must have sound fundamentals, and ones that only hide or obfuscate minting bots or other issues are not real solutions, and therefore should not be implemented. See the [Lessons Learned](#lessons-learned) section for more examples of this.

#### 5. Flexible

In some situations, a project may desire to mint in a way that is highly centralized or in some other non-traditional manner. An example of this would be a project that utilizes in-person minting at an event. In this case, the project may choose to mint from a single, centralized mobile device, but should be transparent about that decision.

## "Fairness" Ideals

Fairness is a concept that is often discussed in the context of minting, and is worth investigating in some amount of nuance.

In an abstract sense, fairness is easy to define. Merriam-Webster defines fairness as:

> "marked by impartiality and honesty: free from self-interest, prejudice, or favoritism".

In practice, however, fairness of a project's mint is much more difficult to define. In one sense, Art Blocks drops are _entirely fair_:

- Open sale at a defined price or auction
- Mint success is determined by transaction time/order
- Transaction confirmation time is determined by the network's gas price auction

In another sense, there are many different ways to define fairness, and each definition has its own set of tradeoffs. In general, we believe there are a few types of fairness that are important to consider when an artist is considering how to distribute their project to collectors:

#### 1. Capitalist Fairness

Capitalist fairness suggests that those who are willing to pay the most for a given drop should be the ones who are able to participate.

An example of a drop paradigm that is capitalist fair is a Dutch auction. In a Dutch auction, the price of a generative art piece starts high, and decreases over time until a collector is willing to pay the price. This ensures that the collector who is willing to pay the most for a generative art piece is the one who is able to mint it.

#### 2. Insider Fairness

Insider fairness suggests that those within an existing community should be the ones who are able to participate.

An example of a drop paradigm that is insider fair is an allowlist. In that paradigm, a collector must have reached out to an artist before the project was released to be allowed to mint. This ensures that the collector who is most involved and interested in a community is the one who is able to mint a generative art piece.

#### 3. Communist Fairness

Communist fairness suggests that all collectors should have an equal chance to participate, regardless of their technical skills or willingness to pay.

An example of a drop paradigm that optimizes for communist fairness would be a pure lottery, where all collectors have an equal chance to mint a generative art piece. This ensures that all collectors have an equal chance to mint a generative art piece.

## Fairness in Practice

In practice, it is difficult to achieve any of the above definitions of fairness in a pure sense. For example, a pure lottery is not possible on Ethereum, because the network is not able to discern humans from bots, and therefore a pure lottery would be susceptible to bots spamming entries and disproportionately winning the lottery.

Art Blocks aims to provide a variety of minting options for artists to choose from, each with their own set of tradeoffs. We believe that artists should be able to choose the minting paradigm that best fits their project's goals.

The minters provided by Art Blocks are intended to follow our design principles while also achieving some kind of fairness. However, each minter's amount of fairness and suceptibility to bots will vary based on:

- project demand/hype
- project price
- market conditions
- gas prices
- etc.

For example, if a highly-anticipated project is sold at a low fixed-price, it is likely that bots will be able to mint a large number of generative art pieces. However, if a less-anticipated project is sold at a fixed-price, it is likely that bots will not mint a large number of generative art pieces because the speculative value of the generative art piece is not high enough to flip for a short-term profit.

The minters provided by Art Blocks are not inherently fair or unfair in nature, but that when used carefully, they can provide a minting experience that stays true to our principles while also providing some amount of fairness. We believe that it is important for artists to understand the tradeoffs of each minter, and to choose the minter(s) that best fits their project's goals.

## Minter Suite

The minter suite is a collection of smart contracts that aim to provide different options for artists to distribute their project's tokens to collectors. A variety of minters are available for artists to choose from that can be used to create a variety of different minting experiences. The minters are designed to be flexible and extensible, but also to provide a consistent and familiar minting experience for collectors.

The shared minter suite is used by Art Blocks, and is also available for use with Art Blocks Engine contracts (V3 only).

More details will be added regarding the shared minter suite in the future, but for now, please see the [Shared Minter Suite](./shared-minter-suite) page for an overview of all available flagship minters at this time.

## Lessons Learned

Below is a collection of lessons that we have learned from our experience with minting generative art pieces on Ethereum.

### One mint per wallet does not prevent bots (without an allowlist)

In the past, we have implemented a "1 mint per wallet" rule, which was intended to prevent bots from minting a large number of generative art pieces. However, this rule was not effective, and actually gave an advantage to bots.

For a botter, minting from 1 or 100 wallets is nearly the same difficulty. However, for a typical collector not using bots, minting from multiple wallets adds a lot of difficulty. Ultimately, the "1-per" restriction puts the average collector at a huge disadvantage relative to a botter.

The "1 mint per wallet" rule is also somewhat misleading because it may lead collectors to believe that a project's distribution is well-diversified, when in reality, it might only be owned by a network of bots operating at many addresses.

In the end, this rule was not effective, harmed less-technical collectors, and was therefore abandoned.

> Note: Limiting the number of mints per wallet on an allowlist is a different paradigm, and is a valid way to limit the number of mints per wallet.

### Disabling minting from smart contracts does not prevent bots

In the past, we have implemented a rule that prevented minting from smart contracts. This was intended to prevent bots from minting a large number of generative art pieces. However, this rule was not effective, because bots are able to mint from EOAs (externally owned accounts), and therefore are still able to mint a large number of generative art pieces.

The "no minting from smart contracts" rule is also somewhat misleading because it may cause collectors to believe that a project's was bot-resistant, when in reality, it is not an effective way to prevent bots from minting.

In the end, this rule was not effective, harmed collectors that wanted to mint from a smart contract (including from security-forward multi-sig wallets such as Gnosis Safe), and was therefore abandoned.

### One mint per transaction does not prevent bots

This is a rule that is implemented by some NFT projects, and is intended to prevent bots from minting a large number of generative art pieces. However, this rule is not effective, because bots are able to mint a large number of generative art pieces by submitting multiple transactions to the network's pending transaction pool.

Additionally, most implementations of this rule prevent minting from smart contracts, which is harmful to collectors that want to mint from multi-sig wallets. Other solutions require collectors to pay for additional gas fees for on-chain storage to support the rule's logic, which is also harmful to collectors.

In the end, this rule is not effective, harms less-technical and/or security-conscious collectors, and was therefore abandoned.

### Low, fixed prices favor bots

In general, low, fixed prices favor bots because they are able to mint a large number of generative art pieces and flip them for a short-term profit. This is especially true when the project is highly-anticipated, and when the project's generative art pieces are expected to have a high speculative value.

Bots have a large advantage over humans when it comes to minting at low, fixed prices, because they are able to submit transactions to the network's pending transaction pool at a high rate, and are able to pay high gas prices to ensure that their transactions are confirmed quickly.

In general, we recommend that artists consider using a Dutch auction or an allowlist to mitigate the effects of bots when minting at low, fixed prices.
