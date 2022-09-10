# FAQs

- [What are the Art Blocks Engine offerings?](https://github.com/ArtBlocks/artblocks-docs/edit/main/art-blocks-engine-onboarding/art-blocks-engine-101/faqs.md#what-are-the-art-blocks-engine-offerings)
- [What's included with Art Blocks Engine?](https://github.com/ArtBlocks/artblocks-docs/edit/main/art-blocks-engine-onboarding/art-blocks-engine-101/faqs.md#what-are-the-current-art-blocks-engine-offerings)
- [What effect does ‘locking’ a project have?](https://github.com/ArtBlocks/artblocks-docs/edit/main/art-blocks-engine-onboarding/art-blocks-engine-101/faqs.md#what-effect-does-locking-an-art-blocks-engine-project-have)
- [How can we add more team members to Discord?](https://github.com/ArtBlocks/artblocks-docs/edit/main/art-blocks-engine-onboarding/art-blocks-engine-101/faqs.md#how-can-we-add-more-team-members-to-discord)
- [How long will the process take from start to public launch?](https://github.com/ArtBlocks/artblocks-docs/edit/main/art-blocks-engine-onboarding/art-blocks-engine-101/faqs.md#how-long-will-the-process-take-from-start-to-public-launch)
- [What information do we need to provide?](https://github.com/ArtBlocks/artblocks-docs/edit/main/art-blocks-engine-onboarding/art-blocks-engine-101/faqs.md#what-information-do-we-need-to-provide-to-deploy-our-smart-contracts)
- [Does Art Blocks create a front-end site for our project?](https://github.com/ArtBlocks/artblocks-docs/edit/main/art-blocks-engine-onboarding/art-blocks-engine-101/faqs.md#does-art-blocks-create-a-front-end-site-for-our-project)
- [How long will each stage of the process take?](https://github.com/ArtBlocks/artblocks-docs/edit/main/art-blocks-engine-onboarding/art-blocks-engine-101/faqs.md#how-long-will-each-stage-of-the-process-take)
- [Core contract vs. Minter contract?](https://github.com/ArtBlocks/artblocks-docs/edit/main/art-blocks-engine-onboarding/art-blocks-engine-101/faqs.md#core-contract-vs-minter-contract)
- [How do we list Art Blocks Engine pieces on OpenSea?](https://github.com/ArtBlocks/artblocks-docs/edit/main/art-blocks-engine-onboarding/art-blocks-engine-101/faqs.md#how-do-we-list-art-blocks-engine-pieces-on-opensea)
- [What's the difference between a testnet token and a mainnet token?](https://github.com/ArtBlocks/artblocks-docs/edit/main/art-blocks-engine-onboarding/art-blocks-engine-101/faqs.md#whats-the-difference-between-a-testnet-token-and-a-mainnet-token)

## What are the Art Blocks Engine offerings?

**Art Blocks Engine:**   
The same flagship product used by Art Blocks for on-chain storage of generative systems. Projects can either use no dependencies or one dependency from a short list of highly decentralized libraries.

[Check this link](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/#limited-dependencies) for a complete list of allowed dependencies.


**Art Blocks Engine Flex:**   
Our newest offering allows generative systems to reference off-chain assets stored on [IPFS](https://ipfs.io/) or [Arweave](https://www.arweave.org/). This means generative systems can use photography, AI, GAN, and other creative tools that are otherwise impractical.

If you’re unsure which offering better fits your needs, get in touch, and we can chat through the benefits of each approach. 

## What's included with Art Blocks Engine?

For a new partnership, the standard current Art Blocks Engine offerings include:

1. Deployment of basic Engine smart contracts suite to testnet and mainnet (includes ETH gas costs incurred for contract deployments):
   1.1 `GenArt721CoreV2` contract: main Engine contract
   1.2 `GenArt721Minter` contract: minting contract, which supports minting in ETH and ERC20 tokens–can be upgraded in the future
   1.3 `Randomizer` contract: basic randomizer, which provides additional entropy to the core contract for token creation–can be upgraded in the future
2. Integration of deployed Core contract with decentralized Graph indexing architecture on testnet and mainnet (includes GRT costs incurred for subgraph update deployment).
3. Integration of deployed contracts and subgraph with Art Blocks’ project setup site, and with Art Blocks’ rendering and metadata infrastructure, on testnet and mainnet. APIs provided will include: 
   * Token API
   * Generator API
   * Rendered Image API

## What effect does ‘locking’ a project have?

Locking a project (specifically on GenArt721CoreV2) permanently freezes the artist name, project name, project scripts, project license, and project IPFS hash on the blockchain. Additionally, maximum invocations of a project can never be increased.

 **Locked projects can not be unlocked**

A summary of how the smart contract functions behave:
- `toggleProjectIsLocked`
  - only callable by admin whitelisted wallets on the core contract
  - can only lock projects (i.e. **locked projects can not be unlocked**)
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
    - before being locked, maximum invocations may be increased
    - after being locked, maximum invocations may only be decreased

## How can we add more team members to Discord?

Contact your account manager for an active invite link to the private Discord server.

## How long will the process take from start to public launch?

The process typically takes 10 weeks from our first conversation until your first public launch. 

However, several factors will likely delay the process. To reduce delays, we recommend:
- Having a front-end developer ready
- Having an artist lined up or generative script ready
- Having a go-to-market strategy ready
- Allocating sufficient time for your team to get fully onboarded - specifically steps 7, 8, and 10 of the [onboarding process](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/Engine-partner-onboarding-steps/).

## What information do we need to provide to deploy our smart contracts?

To get started, you'll provide our team with:

- **An Ethereum wallet address** that you own and will use to manage your Art Blocks Engine smart contracts.
- **The name you’ll use for tokens** from your contract (e.g., for Art Blocks, it is "Art Blocks")
- T**he ticker symbol you’ll use for tokens** from your contract (e.g., for Art Blocks, it is "BLOCKS")

Note: We cannot deploy your contract until you provide the above information. **The name and symbol tied to your contract cannot change once it’s set.**

## Does Art Blocks create a front-end site for our project?

No, partners are responsible for creating and designing their customer-facing experience. 

However, we do have a front-end template with all the web3 connectivity you need to launch. You will still be responsible for branding/designing the template, but this significantly reduces the time needed to complete a front-end. 

## How long will each stage of the process take?

1. Initial outreach - **1-2 weeks**
2. Project scope - **1-2 weeks**
3. Contract agreement - **1 week**
4. Smart contract details - **1-2 days**
5. Contract configuration & testnet deployment - **1 week**
6. Testnet infrastructure integration -** 1 week**
7. Integration with partner’s site - **Varies** (dependent on partner)
8. Test mints on partner site - **Varies** (dependent on partner) 
9.  Deployment to mainnet - **1-2 weeks**
10. Mainnet infrastructure integration -** Varies** (dependent on partner)
11. Mint #0 - **Instant**
12. Project launch! - **1 week** after step 11

## Core contract vs. Minter contract

**Core contract:**
This is the smart contract that controls the artwork created by the artist. No financial transactions occur on this smart contract.

**Minter contract:**
These smart contracts receive funds and split them between the artist(s) and the platform. Artists receive funds directly from these contracts.

## How do we list Art Blocks Engine pieces on OpenSea?

OpenSea will automatically detect and display projects on your contract as one large collection. If you’d like each project to have its own storefront, please contact account manager to facilitate the change. 

## What's the difference between a testnet token and a mainnet token?

**Testnet tokens are free, unlimited, and worthless.** They only exist as a tool for the testing environment before spending actual money (Ether) deploying on Ethereum’s mainnet. 
