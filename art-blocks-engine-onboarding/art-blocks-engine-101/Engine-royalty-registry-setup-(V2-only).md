---
order: 500
---

# Art Blocks Engine Royalty Registry Setup (V2 contracts only)

## Royalty Registry

The [Royalty Registry](https://royaltyregistry.xyz/lookup) is an on-chain tool used by many marketplaces ((soon) OpenSea, Coinbase NFT, etc.) to query royalty payment addresses and percentages when a token is sold. The Royalty Registry lives on the Ethereum blockchain and is decentralized.

!!!danger
Art Blocks Engine contracts integrate with the Royalty Registry directly to handle many projects and artists on a single contract. Please do not use the [Royalty Registry's "Configure" UI](https://royaltyregistry.xyz/configure) to configure the royalties for your Engine contracts. Doing so will result in incorrect royalty payments across many projects. Instead, see the documentation below.
!!!

!!!info
Note that the [Royalty Registry's "Lookup" UI](https://royaltyregistry.xyz/lookup) is a great tool for confirming that your Engine contracts are configured correctly after the configuration steps below have been completed.
!!!

## Royalty Payment Addresses

For Engine contracts, the following addresses may receive royalties:

| Party                        | Typical Royalty Percentage                                     |
| ---------------------------- | -------------------------------------------------------------- |
| Platform (Engine Partner)    | default 2.5%                                                   |
| Render Provider (Art Blocks) | default 2.5%                                                   |
| Artist                       | typically 5%, but configurable by artist                      |
| Additional Payee             | split between Artist & Additional Payee varies across projects |

## Configuring Royalties

V3 and V2 Engine contracts are configured differently. V3 Engine contracts are the latest version of the Art Blocks Engine contracts. Since they were designed after the Royalty Registry was released, they automatically integrate with with the Royalty Registry. V2 Engine contracts also integrate with the Royalty Registry, but have a shim-layer that must also be configured. This is because V2 Engine contracts were designed before the Royalty Registry was released.

## Configuring V3 Engine Contracts

Simply configure the relevant royalty payment details on the token contract itself:

**admin (contract-wide):**

- Ensuring platform and render provider payment addresses are correct, updateable by contract admin by calling `updateProviderSalesAddresses` on the Engine core contract
- Ensuring platform and render provider payment percentages are correct, updateable by contract admin by calling `updateProviderSecondarySalesBPS` on the Engine core contract

**artist (project-specific):**

- Ensuring the project's artist royalty percentage is correct, updateable on the website by the artist in their project dashboard.
- Ensuring the project's artist and additional payee splits are correct, updateable on the website by the artist in their project dashboard.

## Configuring V2 Engine Contracts

### Required V2 Setup

The following steps are required before Art Blocks Engine contracts will integrate properly with the Royalty Registry.

**A. Pre-setup:**

- Ensure every project has the desired artist royalty percentage set on the Engine contract.
  - IMPORTANT: This percentage represents the percentage of the total token sale that will be paid to a combination of artist & additional payee. It is typically 5%. Additionally, the default 2.5% to the Engine platform (you) and 2.5% to render provider (Art Blocks) will be also added by the Royalty Registry override contracts below.
  - **Only artists** may update their project's royalty percentage. They can call `updateProjectSecondaryMarketRoyaltyPercentage(<_projectId>, <_royaltyPercentage>)` on the Engine contract from their artist wallet. Typically royalty percentage would be the number 5, representing 5%.
    > **Note:** This percentage is different than what OpenSea has asked us to do with their off-chain royalty system. In the old system, typically 5%+2.5%+2.5%=10% was set on OpenSea's website because they only supported bulk payments to a single address. In the new on-chain system, payments to more than a single address will be supported.

**B. Royalty Registry Integration:**

1. Create a new override on the Royalty Registry for your Engine core contract
   - View the Royalty Registry's mainnet registry contract on etherscan: [https://etherscan.io/address/0xad2184fb5dbcfc05d8f056542fb25b04fa32a95d#writeProxyContract](https://etherscan.io/address/0xad2184fb5dbcfc05d8f056542fb25b04fa32a95d#writeProxyContract)
   - Using the `Connect to Web3` button, connect your Engine `admin` wallet to etherscan when on the "Write as Proxy" tab.
   - Call the `setRoyaltyLookupAddress` function with the following arguments:
     - `tokenAddress`: The address of your Engine core contract
     - `royaltyLookupAddress`: The address of the standard Art Blocks Engine Royalty Registry override contract, [0x31E1cC72E6f9E27C2ECbB500d978de1691173F5f](https://etherscan.io/address/0x31e1cc72e6f9e27c2ecbb500d978de1691173f5f#code)
2. Set your Platform royalty payment address
   - Connect your Engine `admin` wallet to the Art Blocks Engine royalty override contract, [0x31E1cC72E6f9E27C2ECbB500d978de1691173F5f](https://etherscan.io/address/0x31e1cc72e6f9e27c2ecbb500d978de1691173f5f#writeContract), on etherscan
   - Call the `updatePlatformRoyaltyAddressForContract` function with your Engine token contract address as `_tokenContract`, and your desired platform royalty payment address as `_platformRoyaltyAddress`

Now you will automatically be receiving royalties from sales on secondary markets that support use of the Royalty Registry!

### Optional V2 Configuring

Royalty percentages of 2.5% are used by default by the Art Blocks Engine royalty override contract. The `admin` of any given Engine core contract can override these percentages by calling `updatePlatformBpsForContract` or `updateRenderProviderBpsForContract` on the Art Blocks Engine royalty override contract, [0x31E1cC72E6f9E27C2ECbB500d978de1691173F5f](https://etherscan.io/address/0x31e1cc72e6f9e27c2ecbb500d978de1691173f5f#writeContract), on etherscan

> Note that royalty proportions are defined in terms of Basis points. For example, 250 BPS = 2.5% royalty. See [this article](https://www.investopedia.com/terms/b/basispoint.asp) for more information.

After initial setup, the Platform (Engine partner) royalty payment address may be updated at any time by the `admin` of a given Engine core contract by calling the `updatePlatformRoyaltyAddressForContract` function on the Art Blocks Engine royalty override contract, [0x31E1cC72E6f9E27C2ECbB500d978de1691173F5f](https://etherscan.io/address/0x31e1cc72e6f9e27c2ecbb500d978de1691173f5f#writeContract), on etherscan
