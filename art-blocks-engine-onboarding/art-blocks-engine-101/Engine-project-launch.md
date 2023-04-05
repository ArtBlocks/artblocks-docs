---
order: 800
---
# Art Blocks Engine Project Launch

A high-level overview of launching new projects on a new Art Blocks Engine contract.

---

After deploying an Engine contract, you can now create projects on your contract.

To create a new project shell, use the `addProject` method of your deployed Core Contract. This can be done by connecting to the contract via Etherscan.

For a more in-depth guide on creating new projects on your Engine contract, please see the ["Project Shell Deployment Guide"](adding-new-project-shells.md).

## Pre-mint-#0 Flight Check

Before minting your first token (#0) on your new project shell, please verify the following.

1. The `baseTokenURI` has been set, taking the format of `http://token.artblocks.io/{CORE_CONTRACT_ADDRESS}/`.
2. The max invocations for the project have been set **on the minter**. This is achieved by calling the `setProjectMaxInvocations` on the Minter contract when connecting with Etherscan, with the project ID of the project to be minted as the parameter. **Note**: This should only be done _after_ setting this max invocations for the project on the Core Contract itself.
3. Perform a test-mint in each currency the project accepts (e.g. if the project is planned to use both ETH and some custom ERC20 token for separate stages of the launch, ensure that **both** minting flows are empirically verified).

## Pre-launch (pre-open-minting) Flight Check

Prior to launching your token for open minting, please verify the following:

1. The project has been activated by the contract admin. This can be verified by reading the `projectTokenInfo` field.
2. The project is not yet unpaused. Project pause status is toggleable by the project artist. This can be verified by reading the `projectScriptInfo` field.

## Configure minter and project details for each project on Etherscan
For Engine and Flex Engine V3 contracts, the artist's wallet needs to set up minters for each project individually.

First, assign the minter to your project by using the `MinterFilterV1` contract found in your deployment file. The artist's wallet should use function #6 on the contract, entering the `_projectID` and `_minterAddress`. You can find the minter address in your deployment log, which is pinned in your partner channel.

Once the minter is linked to your project, set the project details on the minter contract. The deployed minter addresses can be found in your deployment file.

For example, if Art Blocks deployed a Dutch Auction with a settlement minter for your core contract, navigate to the `MinterDAExpSettlementV2` contract linked to your core contract. Then, use function #13 to enter details like `_projectId`, `_auctionTimestampStart`, `_priceDecayHalfLifeSeconds`, `_startPrice`, and `_basePrice`. Make sure this is done using the artist's wallet.
