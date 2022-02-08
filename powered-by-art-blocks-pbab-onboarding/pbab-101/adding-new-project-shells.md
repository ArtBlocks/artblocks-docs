---
order: 700
route: /creator-docs/powered-by-art-blocks-pbab-onboarding/pbab-101/adding-new-project-shells/
---
# Project Shell Deployment Guide

An overview of how to deploy a new project on your custom PBAB contract.

1. Collect 3 pieces of information for the to-be-deployed project on your PBAB contract.
   1. The project title (e.g. "Fun Lines")
   2. The artist wallet address, this will determine which address has access to configure the project from within the Art Blocks artist interface, (e.g. `0x78592a6fBE68fEBf226040a5D25ad7e69F2FeAb6`).
   3. The price-per-mint, this will need to be specified [**in WEI**](https://eth-converter.com), (e.g. `350000000000000000`, which is 0.35 in ETH).
2. Navigate to your PBAB Core Contract on Etherscan (e.g. https://ropsten.etherscan.io/address/0x06710498339b30834653459Ac90F52Cbd2F1D085#code).
3. Navigate to the "Write contract" tab and connect your wallet to Etherscan.![](/static/screenshot3.png)
4. Use the `addProject` method to create a new project shell, specifying the information initially collected (as defined in 1. above).
5. Once 4. has been completed, when connected to the Art Blocks website (https://artist-staging.artblocks.io for Ropsten, and https://artblocks.io for mainnet), **with the artist wallet** used in step 4., your artist should be able to begin entering their project details.
   * If you are having trouble finding your project on the Ropsten Art Blocks site, you should be able to navigate to it directly with by entering in your browser a URL of the format: `https://artist-staging.artblocks.io/project/{CONTRACT_ADDRESS}-{PROJECT_ID}` (e.g. for the first project shell on your PBAB core contract, the `{PROJECT_ID}` would be `0`, then `1`, then `2`, etc.).
   * If you are having trouble seeing your project on the corresponding-network's Art Blocks site, first try disconnecting and reconnecting your wallet to the site, ensuring that you are connected with the previously specified artist wallet.
   * When asked to provide the `baseTokenURI` for your project, this should be `https://token.artblocks.io/{CONTRACT_ADDRESS}/`, where `{CONTRACT_ADDRESS}` is the address of **the core contract** for your PBAB project (e.g. `0x06710498339b30834653459Ac90F52Cbd2F1D085` for the project linked above in step 2.). For the Ropsten testnet, this should be `https://token.staging.artblocks.io/{CONTRACT_ADDRESS}/`.
   * Generally speaking, the [Art Blocks 101 for Creators guide](/readme.md) should be broadly applicable to this onboarding step for PBAB-partner-platform artists.
