# FAQs

Frequently asked questions.

## What are the current PBAB offerings?

For a new partnership, the standard current PBAB offerings include:

1. Deployment of basic PBAB smart contracts suite, to Ropsten and to mainnet (includes ETH gas costs incurred for contract deployments):
   * `GenArt721CoreV2` contract: main PBAB contract
   * `GenArt721Minter` contract: minting contract, which supports minting in ETH and ERC20 tokens–can be upgraded in the future
   * `Randomizer` contract: basic randomizer, which provides additional entropy to the core contract for token creation–can be upgraded in the future.
2. Integration of deployed Core contract with decentralized Graph indexing architecture, on Ropsten and on mainnet (includes GRT costs incurred for subgraph update deployment).
3. Integration of deployed contracts and subgraph with Art Blocks’ project setup site, and with Art Blocks’ rendering and metadata infrastructure, on Ropsten and mainnet. API’s provided will include:
   * Token API
   * Generator API
   * Rendered Image API

## What effect does locking a PBAB project have?

Locking a project (specifically on `GenArt721CoreV2`) permanently freezes artist name, project name, project scripts, project license, and project ipfs hash on the blockchain. Additionally, maximum invocations of a project can never be increased.

A summary of how the smart contract functions behave:
- `toggleProjectIsLocked`
  - only callable by admin whitelisted wallets on the core contract
  - can only lock projects (i.e. locked projects can not be unlocked)
- The following functionality is only allowed on unlocked projects:
  - `updateProjectName`
  - `updateProjectArtistName`
  - `updateProjectLicense`
  - project script changes:
    - `addProjectScript`
    - `updateProjectScript`
    - `removeProjectLastScript`
    - `updateProjectScriptJSON`
  - `updateProjectIpfsHash`
- The following functionality is affected by a project being unlocked vs. locked:
  - `updateProjectMaxInvocations`
    - prior to being locked, maximum invocations may be increased
    - after being locked, maximum invocations may only be decreased
