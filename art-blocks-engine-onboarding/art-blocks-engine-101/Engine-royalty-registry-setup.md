---
order: 600
---
# Art Blocks Engine Royalty Registry Setup

## Royalty Registry

The [Royalty Registry](https://royaltyregistry.xyz/lookup) is an on-chain tool used by many marketplaces (OpenSea, Coinbase NFT, etc.) to query royalty payment addresses and percentages when a token is sold. The Royalty Registry lives on the Ethereum blockchain and is decentralized.

## Royalties Overview

For Engine contracts, the following addresses may receive royalties:

Party | Address defined: | Royalty Percentage
--- | --- | ---
Platform (Engine Partner) | **defined and configured on Royalty Registry override contract** | default 2.5%, configurable on override contract
Render Provider (Art Blocks) | defined on Engine core contract | default 2.5%, configurable on override contract
Artist | defined on Engine core contract | defined on Engine contract, typically 5%
Additional Payee | defined on Engine core contract | defined on Engine contract

## Required Setup

The following steps are required before Art Blocks Engine contracts will integrate properly with the Royalty Registry.

A. Pre-setup:
  - Ensure every project has the desired artist royalty percentage set on the Engine contract.
    - IMPORTANT: This percentage represents the percentage of the total token sale that will be paid to a combination of artist & additional payee. It is typically 5%. Additionally, the default 2.5% to the Engine platform (you) and 2.5% to render provider (Art Blocks) will be also added by the Royalty Registry override contracts below.
    - **Only artists** may update their project's royalty percentage. They can call `updateProjectSecondaryMarketRoyaltyPercentage(<_projectId>, <_royaltyPercentage>)` on the Engine contract from their artist wallet. Typically royalty percentage would be the number 5, representing 5%.
   >**Note:** This percentage is different than what OpenSea has asked us to do with their off-chain royalty system. In the old system, typically 5%+2.5%+2.5%=10% was set on OpenSea's website because they only supported bulk payments to a single address. In the new on-chain system, payments to more than a single address will be supported.


B. Royalty Registry Integration:
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

## Optional Configuring

Royalty percentages of 2.5% are used by default by the Art Blocks Engine royalty override contract. The `admin` of any given Engine core contract can override these percentages by calling `updatePlatformBpsForContract` or `updateRenderProviderBpsForContract` on the Art Blocks Engine royalty override contract, [0x31E1cC72E6f9E27C2ECbB500d978de1691173F5f](https://etherscan.io/address/0x31e1cc72e6f9e27c2ecbb500d978de1691173f5f#writeContract), on etherscan
>Note that royalty proportions are defined in terms of Basis points. For example, 250 BPS = 2.5% royalty. See [this article](https://www.investopedia.com/terms/b/basispoint.asp) for more information.

After initial setup, the Platform (Engine partner) royalty payment address may be updated at any time by the `admin` of a given Engine core contract by calling the `updatePlatformRoyaltyAddressForContract` function on the Art Blocks Engine royalty override contract, [0x31E1cC72E6f9E27C2ECbB500d978de1691173F5f](https://etherscan.io/address/0x31e1cc72e6f9e27c2ecbb500d978de1691173f5f#writeContract), on etherscan
