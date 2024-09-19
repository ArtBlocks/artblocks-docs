---
order: 851
---

# Shared Minter Suite

This page provides an overview of the Art Blocks Shared Minter Suite, which enables artists to choose how they distribute their artwork to collectors.

The Shared Minter Suite is available for all projects, including Art Blocks Engine projects.

!!!info
For legacy contracts, core contract admins can view the [Minter Migration Runbok](./../art-blocks-engine-onboarding/art-blocks-engine-101/minter-suite-migration-runbook.md) for details about how to migrate to the shared minter suite.
!!!

## Mix-and-Match

Artists can mix-and-match minter options to create a custom minter configuration for their project. For example, an artist could initially use the allowlist minter to allow a specific set of collectors to mint one token per allowlisted wallet, and then could open up minting to the public via a switch to a Dutch auction with settlement minter.

Each minter supports limiting to a certain number of project invocations. For example, an artist could allow Minter A to be used for the first 1000 project invocations, and then switch to Minter B for the remaining project invocations.

## Globally Available Minter Options

The current available Minter options are discussed below. We are continually expanding our shared minter suite over time.

### `Set price - ETH`

The set price minter is used for fixed price releases. It is the simplest minter and prices all tokens at the same price, in ETH.

### `Set price - ETH, allowlisted users only`

Extends the functionality of the `Set price, ETH` minter to allow only wallets on an allowlist to mint. The allowlist can be configured to limit minting to a predetermined list of wallet addresses, and artists can specify the number of mints allowed per wallet.

### `Set price - ETH, token holders only`

Extends the functionality of the `Set price, ETH` minter to allow only holders of a specific ERC-721 token to mint.

### `Set Price - custom ERC20`

Set price in ERC20 is a fixed price minter that allows accepting any ERC20 token as payment for your sale of tokens.

Custom ERC20 tokens can be used for a variety of purposes, including for a "mint pass" style experience.

### `Dutch auction (w/settlement) - exponential price decrease`

When this minter is used, all collectors will pay the same net-price as the final purchaser. This is typically the most fair and equitable Dutch auction type for buyers because all buyers pay the same price, making it a great auction type for many projects.

Collectors who purchase above the lowest price will be able to claim a settlement after the auction. The settlement will be the difference between the price they purchased at and the final purchase price. All funds are held non-custodially by the smart contract until the auction ends and revenues are collected by the artist or admin.

Exponential price curves approximate a constant percent decrease over time, making them a popular choice for Dutch auctions.

!!!info
If an artist reduces the max supply of their project mid-auction, and the project sells out above auction base price, revenues must be withdrawn by core contract admin. This was implemented to protect collectors from an artist unilaterally potentially inflating sellout price during an action, and immediately withdrawing revenues. Admin concurrence is required to withdraw revenues in this case.
!!!

!!!info
For supplemental information about the auction reset process, please see the [Auction Reset Process](./minter-suite-supplemental.md#auction-reset-process) section.
!!!

### `Dutch auction - exponential price decrease`

For Dutch auctions without settlement, artists specify the starting price, ending price, and the half-life for price drops. Collectors will pay more for tokens purchased earlier in the auction, and less for tokens purchased later in the auction.

Exponential price curves approximate a constant percent decrease over time, making them a popular choice for Dutch auctions.

!!!info
For supplemental information about the auction reset process, please see the [Auction Reset Process](./minter-suite-supplemental.md#auction-reset-process) section.
!!!

### `Dutch auction - linear price decrease`

For Dutch auctions without settlement, artists specify the starting price, ending price, and the duration of the auction. Collectors will pay more for tokens purchased earlier in the auction, and less for tokens purchased later in the auction.

Linear price curves provide a constant price decrease over time.

Two price curves are available for Dutch auctions without settlement: exponential and linear. Exponential price curves approximate a constant percent decrease over time, while linear price curves provide a constant price decrease over time.

!!!info
For supplemental information about the auction reset process, please see the [Auction Reset Process](./minter-suite-supplemental.md#auction-reset-process) section.
!!!

### `Dutch auction - exponential price decrease, token holders only`

This minter extends the functionality of the Dutch auction minter to allow only holders of a specific ERC-721 token to mint.

### `Dutch auction - linear price decrease, token holders only`

This minter extends the functionality of the Dutch auction minter to allow only holders of a specific ERC-721 token to mint.

### `Ranked auction`

The Ranked Auction minter allows for a ranked auction process where collectors can submit bids for a limited number of tokens. The highest bidders will receive tokens, while losing bidders will receive a refund.

All winning bids pay the same price, which is the lowest winning bid.

The ranked auction process happens non-custodially on-chain, and is scalable to arbitrarily large projects. Artists may incur gas costs associated with minting tokens for winning bidders.

### `Serial English auction`

The Serial English Auction (SEA) minter allows for a series of English auctions for individual tokens to be run in sequence. The minter was originally inspired by the popular [nouns.wtf](https://nouns.wtf/) project, and was implemented with minor adjustments to provide a seamless experience for Art Blocks artists and collectors.

Artists may configure future token auction parameters, such as starting auction price and minimum auction length. Collectors may then kick off token auctions by submitting a bid for a pre-minted token. Once an auction begins, any wallet may submit a higher bid for the token up for sale. Losing bids are refunded automatically when outbid. If a bid is submitted near the end of an auction, the auction is extended such that a human is able to submit a higher bid, ensuring a human can fairly compete against a bot.

Once an auction is complete, another token auction may be started by any collector submitting a bid for the next token, while also sending the previous auction winner their token.

The minter pre-mints tokens before their auction, so bids are placed on an already-existing token, not on hypothetical tokens.

The minter may be used for any project, and is certainly ideal for projects that have a series of tokens that are released in a sequence. It may also be used to auction off a 1:1 token. The minter is also ideal for projects that have a strong community, as it allows for community members to participate in the auction process over a long period of time, carefully considering each generative output.

Bids and auction parameters are stored on-chain, and the Art Blocks subgraph and API index all historical bids in [`bids_metadata`](https://docs.artblocks.io/public-api-docs/#definition-bids_metadata) as well as auction parameters in [`project_minter_configurations`](https://docs.artblocks.io/public-api-docs/#definition-project_minter_configurations).

### `polyptych (copy-hash) minter`

This minter enables the artist to mint tokens with identical token hashes. This is useful for projects that are intended to be displayed as a polyptych.

This minter allows either artists to mint child tokens to a parent token holder's wallet, or allows the parent token holder to mint child tokens.

An artist's script must work closely with the minter to ensure that the correct frame is used for each token number. For example, if a project has 3 frames, the artist's script must ensure that e.g. tokens 0-99 are minted with frame 1, tokens 100-199 are minted with frame 2, and tokens 200-299 are minted with frame 3. The artist is able to increment the frame number for their project on the minter.

This minter is technically complex, and artists must also configure the shared randomizer when using this minter.

Limited creator dashboard support is available for this minter at this time, so some interactions with the minter must be done via a service such as [Etherscan]](https://etherscan.io/).

Despite the complexity of this minter, the resulting outputs can be very powerful and rewarding for artists and collectors!

### `polyptych (copy-hash) minter, custom ERC20`

This minter extends the functionality of the polyptych minter to allow accepting any ERC20 token as payment for your sale of tokens.

## Custom, One-Off Minters

Engine partners can also create custom, one-off minters for their projects. These minters are only available to projects on the Engine contract that approves them, extending the globally set of available minters for their contract.

For more information about adding custom minters to your Engine contract, please see the [custom minters page](./custom-minters).
