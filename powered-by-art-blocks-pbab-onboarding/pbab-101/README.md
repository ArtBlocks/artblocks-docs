# PBAB 101

A high level process-map for PBAB onboarding.

1. After the terms of engagement are finalized, you’ll sign the PBAB service and setup agreement. 
2. Provide the following information to Art Blocks for your PBAB project:
   1. The admin address that you would like to have own these contracts. This address controls the the core contract and the minter.
   2. The name of tokens from your contract (e.g. for Art Blocks it is "Art Blocks" https://etherscan.io/address/0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270#code).
   3. The ticker for tokens from your contract (e.g. for Art Blocks it is "BLOCKS" https://etherscan.io/address/0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270#code).
3. Art Blocks' will deploy a set of Ropsten smart contracts for your team to begin integrating with.
   * After Ropsten deployment, there are two steps that may proceed in parallel.
     1. Your team can integrate their frontend to allow for minting via your new PBAB smart contract (using deployed Ropsten smart contracts).
     2. Art Blocks will need to integrate your newly deployed Ropsten smart contracts with the Art Blocks rendering infrastructure on Ropsten, after which your team will be able to connect to the https://artist-staging.artblocks.io site and interact with projects on the Ropsten network that you created on your PBAB smart contract, as if those projects were on Art Blocks itself (e.g. upload source code, set features, set project metadata, etc.).
        * An ETA for this infrastructure integration piece will be given at the time of Ropsten contract deployment. On average, this will take 1 week from the time of Ropsten deployment.
        * To create a new project shell, you should use the `addProject` method of your newly deployed PBAB Core Contract. This can be done by connecting to the contract via Etherscan.
4.  Your team will integrate a custom web frontend with your deployed PBAB smart contracts (e.g. **implementing their own purchase + display flow**) and with the Art Blocks API as needed. An example of frontend purchase flow logic is provided here as a reference for integrating partners:

<details>
  <summary>Click me</summary>
  
  ### Heading
  1. Foo
  2. Bar
     * Baz
     * Qux

  ### Some Code
  ```js
  function logSomething(something) {
    console.log('Something', something);
  }
  ```
</details>
   
5. Your team will use https://artist-staging.artblocks.io site to configure all project metadata details (e.g. project description, license associated with outputs,  artist website) and upload your project script source code. This process looks very similar to the process within Art Blocks itself for creators uploading their projects, so "[Art Blocks 101 for Creators](../../creator-onboarding/readme/readme.md#documentation)" should provide a good reference for this process. If you need help along the way, the Art Blocks team will help guide you through the process.
6. Once you've fully completed the setup and testing process for **any** PBAB project on your platform, you can request a project script audit from Art Blocks to guaruntee resolution-agnositicism and determinism. **Warning**: if you'd like to opt-out of this step, it may result in undiagnosed issues with the rendered outputs of an unaudited project due to not conforming to Art Blocks' resolution-agnositic and deterministic standards (e.g. they perform differently on different screen sizes, different devices different operating systems, or are different from view-to-view).
7. After the entire end-to-end integration has been vetted on Ropsten, the above process may proceed on mainnet. Vetting includes minting in each minting format, from the PBAB partner's frontend minting experience, while integrated with the Art Blocks' provided rendering infrastructure, etc.
8. Repeat the above process, for mainnet deployment. In summary, mainnet deployment entails:
   1. Deploy mainnet contracts.
   2. Integrate mainnet contracts with Art Blocks' rendering and API infrastructure.
   3. Update your mainnet website implementation to reference deployed mainnet contracts.
   4. Create a new mainnet project shell on your smart contract (using `addProject`) and upload all project details and project script using the artist interface at https://artblocks.io.
   5. Mint at least one piece (mint #0) in a controlled environment on mainnet, being sure to mint in each format you plan to for your open release.
9. After the above has all been performed, you should run through the following "pre-flight" checklist and ensure there are no loose threads:
   * If accepting ETH, check that the wallets **are not** multisig wallets like Gnosis Safe (check the minter owner, render provider, artist, and any additional payee).
     * **Note: **It is possible to use multisig wallets if our client's front-end properly populates [access lists](https://docs.ethers.io/v5/api/providers/types/#providers-AccessList) in their front end, but minting from Etherscan will not work.
   * **Especially important for mainnet**: Test-mint a token in each currency that will be accepted for a project (e.g. if ETH is used for part of the sale, and a custom ERC20 is used for a separate part of the sale). Verify that your front-end is used to successfully mint in each currency to ensure a proper end-to-end test.
   * If actions of whitelisting/removing minters are expected, test those actions.
   * If actions of changing max invocations are expected, test those actions.
   * When using PBAB's front-end to mint, ensure at least a **10%** margin is being added to each transaction's [estimated Gas Limit](https://docs.ethers.io/v5/api/providers/provider/#Provider-estimateGas), as originated by the your fronend logic.
     * If 0% margin is used during a live NFT sale, the blockchain state is likely to change between a user-submitted transaction and when it's mined. Small changes in required Gas Limit are likely, and will result in transaction failure if required gas increases.
10. You are now ready to sync with the Art Blocks team on planning for a launch date, that is at least 1 week out from the time the above steps have all been completed.
