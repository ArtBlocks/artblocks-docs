---
order: 800
---

# Engine Project Deployment and Launch Guide

This guide provides basic instructions for deploying and launching a new project on the V2 and V3 Engine smart contracts. You will learn how to create a project shell, assign a minter to each project, and setup the necessary configurations before minting and launching your project. This documentation aims to simplify the process and ensure a smooth project launch on the Art Blocks Engine platform.

There are slight variations between V2 and V3 contracts, which will be noted in the relevant sections. 

## Project Shell Deployment

[!embed](https://www.loom.com/embed/9cb61eef17724107a6e7916d682c8bd5)

1.  Collect the required information for the project:
    -   Project title (e.g., "Fun Lines")
    -   Artist's wallet address (e.g., 0x78592a6fBE68fEBf226040a5D25ad7e69F2FeAb6)
    -   (V2 only) Price-per-mint specified in WEI (e.g., 350000000000000000, or 0.35 ETH)
2.  Navigate to your Engine Core Contract on Etherscan and connect your wallet. You can find this link in your `DEPLOYMENTS.md` log. [https://goerli.etherscan.io/address/0xd2363Acbf8CdF01A5FdfcB8f0295e0a5dF94518D#code](https://goerli.etherscan.io/address/0xd2363Acbf8CdF01A5FdfcB8f0295e0a5dF94518D#code)) 
    
3.  Click the "Write contract" tab and use the `addProject` method to create a new project shell, specifying the information collected in step 1.
    
4.  Connect to the Art Blocks website with the artist wallet used in in Step 3. Your artist should be able to begin entering project details.

	Testnet URL: `https://artist-staging.artblocks.io/engine/[flex OR fullyonchain]/projects/[coreContractAddress]/[projectID]` 
	example: https://artist-staging.artblocks.io/engine/flex/projects/0x28b82AA5bb6d00363ae0FBC5ecaD689Ae49BC82B/0

	Mainnet URL: `https://www.artblocks.io/engine/[flex OR fullyonchain]/projects/[coreContractAddress]/[projectID]`
	example: https://www.artblocks.io/engine/fullyonchain/projects/0xa319C382a702682129fcbF55d514E61a16f97f9c/1
    
5.  If you encounter issues finding or seeing your project on the Art Blocks site, disconnect and reconnect your wallet, ensuring you are connected with the previously specified artist wallet.

## Assigning a Minter (V3 only)

[!embed](https://www.loom.com/share/66f542b3ef024f7c80059115e76bae8d)

Minters are assigned on a per-project basis on V3 contracts, and minters must be assigned by the **artist's wallet**. For the artist wallet to assign a minter, follow these steps: 

1.  Assign the minter to your project by using the `MinterFilterV1` contract found in your deployment file. The artist's wallet should use function #6 `setMinterForProject`, entering the `_projectID` and `_minterAddress`. You can find the minter address in your deployment log, which is pinned in your partner channel.
    
2.  Once the minter is linked to your project, set the project details on the minter contract. The deployed minter addresses can be found in your deployment file.

	For example, if Art Blocks deployed a Dutch Auction minter for your core contract, navigate to the  `MinterDAExpV4`  contract on Etherscan (in your `DEPLOYMENT.md` log). Then, use the function `setAuctionDetails` to enter details like  `_projectId`,  `_auctionTimestampStart`,  `_priceDecayHalfLifeSeconds`,  `_startPrice`, and  `_basePrice`. Make sure this is done using the artist's wallet.
    

## Pre-mint-#0 Flight Check

Before minting your first token (#0) on your new project shell, verify the following:

1.  The baseTokenURI has been set, following the format:
- Mainnet: http://token.artblocks.io/{CORE_CONTRACT_ADDRESS}/
- Testnet: https://token.staging.artblocks.io/{CONTRACT_ADDRESS}/
2.  The max invocations for the project have been set. (note: project size **cannot** be increased once set on V3 contracts)
3. Mint through your own front end. On testnet, you'll want to test each minter type and currency you plan to use on mainnet.

## Pre-launch (pre-open-minting) Flight Check

For a project to be avaialble for public purchase, the project must be activated by the admin, and unpaused by the artist.

tldr:
inactive + paused (default state) = private project shell and unable to purchase
active + paused = public project shell and ***only*** the artist wallet can purchase
active + unpaused = open to purchase

Before launching your project for open minting, verify the following:

1.  The project has been activated by the contract admin.
2.  The project is not yet unpaused.

Once unpaused the project will be open, depending on the minter being used (DA will not open until specified `startTime`)

[!embed](https://www.loom.com/share/65a8e19513944d3c9a39952696c11f43)
