---
order: 851
---

# Shared Minter Suite

This page provides an overview of the Art Blocks Shared Minter Suite, which enables artists to choose how they distribute their artwork to collectors.

The Shared Minter Suite is available for all projects, including Art Blocks Engine projects.

!!!info
Only projects on contracts that have been migrated to the Shared Minter Suite will be able to use the new minter options. Engine core contract admins can view the [Minter Migration Runbok](./../art-blocks-engine-onboarding/art-blocks-engine-101/minter-suite-migration-runbook.md) for more details.
!!!

## Mix-and-Match

Artists can mix-and-match minter options to create a custom minter configuration for their project. For example, an artist could initially use the allowlist minter to allow a specific set of collectors to mint one token per allowlisted wallet, and then could open up minting to the public via a switch to a Dutch auction with settlement minter.

Each minter supports limiting to a certain number of project invocations. For example, an artist could allow Minter A to be used for the first 1000 project invocations, and then switch to Minter B for the remaining project invocations.

## Globally Available Minter Options

The current available Minter options are discussed below. We are continually expanding our shared minter suite over time.

### `Set Price, ETH`

The set price minter is used for fixed price releases. It is the simplest minter and prices all tokens at the same price, in ETH.

### `Set Price, ERC20`

Set price in ERC20 is a fixed price minter that allows accepting any ERC20 token as payment for your sale of tokens. In addition to specifying a fixed price, artists will specify the ERC20 token address for the custom token sale.

Custom ERC20 tokens can be used for a variety of purposes, including for a "mint pass" style experience.

### `Dutch Auction with Settlement - Exponential Price Decrease`

When this minter is used, all collectors will pay the same net-price as the final purchaser. This is typically the most fair and equitable Dutch auction type for buyers because all buyers pay the same price, making it a great auction type for many projects.

Collectors who purchase above the lowest price will be able to claim a settlement after the auction. The settlement will be the difference between the price they purchased at and the final purchase price. All funds are held non-custodially by the smart contract until the auction ends and revenues are collected by the artist or admin.

!!!info
If an artist reduces the max supply of their project mid-auction, and the project sells out above auction base price, revenues must be withdrawn by core contract admin. This was implemented to protect collectors from an artist unilaterally potentially inflating sellout price during an action, and immediately withdrawing revenues. Admin concurrence is required to withdraw revenues in this case.
!!!

!!!info
For supplemental information about the auction reset process, please see the [Auction Reset Process](./minter-suite-supplemental.md#auction-reset-process) section.
!!!

!!!info
For Art Blocks Flagship, please see the [Project Pricing: Dutch Auction Settings](./../creator-onboarding/readme/project-pricing-model.md) section for more information on how to determine the appropriate pricing parameters for your auction.
!!!

### `Dutch Auction without Settlement`

For Dutch auctions without settlement, artists specify the starting price, ending price, and the half-life for price drops. Collectors will pay more for tokens purchased earlier in the auction, and less for tokens purchased later in the auction.

Two price curves are available for Dutch auctions without settlement: exponential and linear. Exponential price curves approximate a constant percent decrease over time, while linear price curves provide a constant price decrease over time.

Variants of this minter are also provided that support limiting purchasing to wallets that hold a token from a specified list of allowlisted Art Blocks or Art Blocks Engine projects.

!!!info
For supplemental information about the auction reset process, please see the [Auction Reset Process](./minter-suite-supplemental.md#auction-reset-process) section.
!!!

### `Set Price, Allowlisted Users Only`

This minter enables the artist to limit minting of their project's tokens to a predetermined list of wallet addresses. Artists upload a list of allowlisted wallet addresses, and may also specify the number of mints allowed per wallet. Mints per wallet can be set to a value, or may be set to unlimited (limited only by project maximum invocations).

Artists are responsible for crafting their allowlist and uploading a comma-separated list of ETH addresses in a .txt or .CSV file to the creator dashboard. These wallet addresses cannot be ENS names, but list the full address of the wallet. [Premint](https://www.premint.xyz/) is a super helpful tool for creating an allowlist by using social channels to reach collectors, friends, family, etc. In addition, Art Blocks hosts a [Python script](https://github.com/ArtBlocks/artblocks-community-tooling/tree/main/SnapshotABHolders) for retrieving & snapshotting either a list of all Art Blocks token holders or the token-holders of a specific project.

Variants of this minter are provided that support purchasing in ETH, or in a custom ERC20 token.

!!!info
Allowlists use Merkle trees, which enables them to be verified on-chain and to be decentralized. It also is efficient, enabling very large allowlists. For example, ~40,000 wallet addresses were used for the Friendship Bracelet project's allowlist.
!!!

!!!info
Note that vault delegation via [Delegate Cash](https://delegate.cash/) is available for the Allowlisted Users minter. Only V1 of the delegation registry is supported at this time. For more details please visit this [video walkthrough](https://www.youtube.com/watch?v=2-AgG--zcaw&list=PLSNTJAzmISeZcLm19EhafsGjJXwwgzBbU&index=5).
!!!

### `Set Price, Token Holders Only`

This minter allows tokens to be minted with ETH when the purchaser owns a token from one or more allowlisted Art Blocks or Art Blocks Engine project. This contract does not track if a purchaser has/has not minted already (ie. a "mint limit" is not available) -- it simply restricts purchasing to anybody that holds one or more of a specified list of ERC-721 NFTs.

Artists may use the artist dashboard to pre-select a list of allowlisted Art Blocks or Art Blocks Engine projects, of which any valid token holders will be able to purchase for the upcoming project. Note that a "snapshot" won't apply to this minter -- after the project has been made public, users can purchase a token from any allowlisted project and mint freely.

!!!info
Note that vault delegation via [Delegate Cash](https://delegate.cash/) is available for the Token Holders Only minter. Only V1 of the delegation registry is supported at this time. For more details please visit this [video walkthrough](https://www.youtube.com/watch?v=2-AgG--zcaw&list=PLSNTJAzmISeZcLm19EhafsGjJXwwgzBbU&index=5).
!!!

### `Set Price, Polyptych`

This minter enables the artist to mint tokens with identical token hashes. This is useful for projects that are intended to be displayed as a polyptych.

This minter allows either artists to mint child tokens to a parent token holder's wallet, or allows the parent token holder to mint child tokens.

An artist's script must work closely with the minter to ensure that the correct frame is used for each token number. For example, if a project has 3 frames, the artist's script must ensure that e.g. tokens 0-99 are minted with frame 1, tokens 100-199 are minted with frame 2, and tokens 200-299 are minted with frame 3. The artist is able to increment the frame number for their project on the minter.

This minter is technically complex, and artists must also configure the shared randomizer when using this minter.

Limited creator dashboard support is available for this minter at this time, so some interactions with the minter must be done via a service such as [Etherscan]](https://etherscan.io/).

Despite the complexity of this minter, the resulting outputs can be very powerful and rewarding for artists and collectors!

## Custom, One-Off Minters

Engine partners can also create custom, one-off minters for their projects. These minters are only available to projects on the Engine contract that approves them, extending the globally set of available minters for their contract.

For more information about adding custom minters to your Engine contract, please see the [Minter Migration Runbok](./../art-blocks-engine-onboarding/art-blocks-engine-101/minter-suite-migration-runbook.md#adding-a-custom-one-off-minter-to-the-shared-minter-suite).
