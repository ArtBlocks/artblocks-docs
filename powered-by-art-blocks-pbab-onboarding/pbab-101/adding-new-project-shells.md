---
order: 700
---
# Project Shell Deployment Guide

An overview of deploying a new project on your custom Art Blocks Engine contract.

1. Collect 3 pieces of information for the to-be-deployed project on your Engine contract.
   1.1 The project title (e.g. "Fun Lines")
   1.2 The artist's wallet address, this will determine which address has access to configure the project from within the artist interface, (e.g. `0x78592a6fBE68fEBf226040a5D25ad7e69F2FeAb6`).
   1.3 The price-per-mint, this will need to be specified [**in WEI**](https://eth-converter.com), (e.g. `350000000000000000`, which is 0.35 in ETH).
2. Navigate to your Engine Core Contract on Etherscan (e.g. https://ropsten.etherscan.io/address/0x06710498339b30834653459Ac90F52Cbd2F1D085#code).
3. Navigate to the "Write contract" tab and connect your wallet to Etherscan.![](/static/screenshot3.png)
4. Use the `addProject` method to create a new project shell, specifying the information collected in step 1 above.
5. Once 4 has been completed, connect to the Art Blocks website  (https://artist-staging.artblocks.io for testnet, and https://artblocks.io for mainnet), **with the artist wallet** used in step 4., your artist should be able to begin entering their project details.
   5.1 If you are having trouble finding your project on the Ropsten Art Blocks site, you should be able to navigate to it directly by entering in your browser a URL of the format: `https://artist-staging.artblocks.io/project/{CONTRACT_ADDRESS}-{PROJECT_ID}` (e.g. for the first project shell on your Engine core contract, the `{PROJECT_ID}` would be `0`, then `1`, then `2`, etc.).
   5.2 If you are having trouble seeing your project on the corresponding-network's Art Blocks site, first try disconnecting and reconnecting your wallet to the site, ensuring that you are connected with the previously specified artist wallet.
   5.3 When asked to provide the `baseTokenURI` for your project, this should be `https://token.artblocks.io/{CONTRACT_ADDRESS}/`, where `{CONTRACT_ADDRESS}` is the address of **the core contract** for your Engine project (e.g. `0x06710498339b30834653459Ac90F52Cbd2F1D085` for the project linked above in step 2.). For the testnet, this should be `https://token.staging.artblocks.io/{CONTRACT_ADDRESS}/`.
   5.4 Generally speaking, the [Art Blocks 101 for Creators guide](/creator-onboarding/readme/readme.md) should be broadly applicable to this onboarding step for PBAB-partner-platform artists.
