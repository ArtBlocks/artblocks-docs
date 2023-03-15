---
order: 851
---

# Minter Suite

This page provides an overview of the Art Blocks Minter Suite, which enables artists to choose how they distribute their artwork to collectors. on a per-project basis.

The current available Minter options are discussed below. We are continually expanding our minter suite over time.

!!!info
For details on determining proper pricing and configuring your project's minter, please see the [Minter section in the Project Form Fields Guide](project-form-fields-guide.md#minter).
!!!

## `Set Price - ETH`

The set price minter is used for fixed price releases. It is the simplest minter and prices all tokens at the same price, in ETH.

## `Dutch Auction with Settlement - Exponential Price Decrease`

When this minter is used, all collectors will pay the same net-price as the last purchaser. This is typically the most fair and equitable Dutch auction type for buyers because all buyers pay the same price, making it the recommended auction type for most projects.

Collectors who purchase above the lowest price will be able to claim a settlement after the auction. The settlement will be the difference between the price they purchased at and the last purchase price. All funds are held non-custodially by the smart contract until the auction ends and revenues are collected by the artist.

!!!info
We are currently rolling this minter out in production. For a period of time, we will continue to allow DAs without settlement, but we would like to move towards all DAs including settlement in the future. It is important to note that we do not expect the overall revenue that artists receive to decrease between this option and the exponential Dutch auction without settlement, due to how blockchain mechanics interact with the Dutch auction mechanics.
!!!

Note that the Dutch auction with settlement minter can be coupled with an allowlist minter. In this case, the allowlist portion of the auction must come before the dutch auction with settlement.

!!!info
For Art Blocks Flagship, please see the [Project Pricing: Dutch Auction Settings](project-pricing-model.md) section for more information on how to determine the appropriate pricing parameters for your auction.
!!!

## `Automated Exponential Dutch Auction`

For exponential Dutch auctions, artists specify the starting price, ending price, and the half-life for price drops. Collectors will pay more for tokens purchased earlier in the auction, and less for tokens purchased later in the auction.

## `Automated Linear Dutch Auction`

For linear Dutch auctions, artists will specify the starting price, ending price, starting time, and ending time of the auction. The price will then gradually decrease each block over the total auction time. Collectors will pay more for tokens purchased earlier in the auction, and less for tokens purchased later in the auction.

## `Set price in Custom ERC20`

Set price in ERC20 is a fixed price minter that allows accepting any ERC20 token as payment for your sale of tokens. In addition to specifying a fixed price, artists will specify the ERC20 token address for the custom token sale.

## `Set Price - ETH, Allowlisted Users Only`

This minter enables the artist to limit minting of their project's tokens to a predetermined list of wallet addresses. Artists upload a list of allowlisted wallet addresses, and may also specify the number of mints allowed per wallet. Mints per wallet can be set to a value, or may be set to unlimited (limited only by project maximum invocations).

Artists are responsible for crafting their allowlist and uploading a comma-separated list of ETH addresses in a .txt or .CSV file to the artist dashboard. These wallet addresses cannot be ENS names, but list the full address of the wallet. [Premint](https://www.premint.xyz/) is a super helpful tool for creating an allowlist by using social channels to reach collectors, friends, family, etc. In addition, Art Blocks hosts a [Python script](https://github.com/ArtBlocks/artblocks-community-tooling/tree/main/SnapshotABHolders) for retrieving & snapshotting either a list of all Art Blocks token holders or the token-holders of a specific project.

!!!info
Allowlists use Merkle trees, which enables them to be verified on-chain and to be decentralized. It also is efficient, enabling very large allowlists. For example, ~40,000 wallet addresses were used for the Friendship Bracelet project's allowlist.
!!!

!!!info
Note that vault delegation via [Delegate Cash](https://delegate.cash/) is available for the Allowlisted Users minter. For more details please visit this [video walkthrough](https://www.youtube.com/watch?v=2-AgG--zcaw&list=PLSNTJAzmISeZcLm19EhafsGjJXwwgzBbU&index=5).
!!!

## `Set Price - ETH, Token Holders Only`

This minter allows tokens to be minted with ETH when the purchaser owns a token from one or more allowlisted Art Blocks or Art Blocks Engine project. This contract does not track if a purchaser has/has not minted already (ie. a "mint limit" is not available) -- it simply restricts purchasing to anybody that holds one or more of a specified list of ERC-721 NFTs.

Artists may use the artist dashboard to pre-select a list of allowlisted Art Blocks or Art Blocks Engine projects, of which any valid token holders will be able to purchase for the upcoming project. Note that a "snapshot" won't apply to this minter -- after the project has been made public, users can purchase a token from any allowlisted project and mint freely.

!!!info
Note that vault delegation via [Delegate Cash](https://delegate.cash/) is available for the Token Holders Only minter. For more details please visit this [video walkthrough](https://www.youtube.com/watch?v=2-AgG--zcaw&list=PLSNTJAzmISeZcLm19EhafsGjJXwwgzBbU&index=5).
!!!
