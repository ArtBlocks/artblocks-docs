---
order: 100
---

# FAQs

- [What are the Art Blocks Engine offerings?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#what-are-the-art-blocks-engine-offerings)
- [What's included with Art Blocks Engine?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#whats-included-with-art-blocks-engine)
- [What effect does ‘locking’ a project have?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#what-effect-does-locking-a-project-have)
- [How can we add more team members to Discord?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#how-can-we-add-more-team-members-to-discord)
- [How long will the process take from start to public launch?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#how-long-will-the-process-take-from-start-to-public-launch)
- [What information do we need to provide?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#what-information-do-we-need-to-provide-to-deploy-our-smart-contracts)
- [Does Art Blocks create a front-end site for our project?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#does-art-blocks-create-a-front-end-site-for-our-project)
- [How long will each stage of the process take?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#how-long-will-each-stage-of-the-process-take)
- [Core contract vs. Minter contract?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#core-contract-vs-minter-contract)
- [How do we list Art Blocks Engine pieces on OpenSea?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#how-do-we-list-art-blocks-engine-pieces-on-opensea)
- [What's the difference between a testnet token and a mainnet token?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#whats-the-difference-between-a-testnet-token-and-a-mainnet-token)
- [Flex: What are the limitations around file size and file type for external assets? How many external assets can a project have?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#flex-what-are-the-limitations-around-file-size-and-file-type-for-external-assets-how-many-external-assets-can-a-project-have)
- [Flex: Can JS external asset dependencies make external calls to other APIs/assets?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#flex-can-js-external-asset-dependencies-make-external-calls-to-other-apisassets)
- [How does project size work on the minterFilter contract vs Core contract?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#how-does-project-size-work-on-the-minterfilter-contract-vs-core-contract)
- [How does `autoApproveArtistSplitProposals` work?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#how-does-autoApproveArtistSplitProposals-work)
- [When should I enable GPU rendering?](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/faqs/#when-should-I-enable-GPU-rendering)

## What are the Art Blocks Engine offerings?

**Art Blocks Engine:**   
Used for on-chain storage of generative systems. Projects can use no dependencies or one dependency from a list of decentralized libraries. [See the allowed dependencies here.](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/#limited-dependencies)


**Art Blocks Engine Flex:**   
Allows generative systems to reference off-chain assets stored on IPFS or Arweave, enabling creative tools like photography, AI, and GAN.

Email us at Engine@artblocks.io to discuss which offering best suits your needs.

## What's included with Art Blocks Engine?

For a new partnership, the standard current Art Blocks Engine offerings include:

1. Deployment of Engine smart contracts suite to testnet and mainnet (includes gas costs).
2. Integration of deployed Core contract with decentralized Graph indexing architecture on testnet and mainnet, includes GRT costs incurred for subgraph update deployment.
3. Integration of deployed contracts and subgraph with Art Blocks' project setup site and rendering/metadata infrastructure (APIs: Token, Generator, Rendered Image).

## What effect does ‘locking’ a project have?

Locking a project (specifically on V2 Contracts) permanently freezes the artist name, project name, project scripts, project license, and project IPFS hash on the blockchain. Additionally, maximum invocations of a project can never be increased.

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

### Changes for V3 contracts (deployed after March '23)

- In addition to the above, artists can update project description when project is unlocked. However, only contract admins can update project the description when the project is locked.
- **V3 contracts autolock four weeks after a project is complete.**

## How can we add more team members to Discord?

Contact your account manager for an invite link to the private Discord server.

## How long will the process take from start to public launch?

The process typically takes 10 weeks from initial conversation to public launch, but is **highly** dependent on partner's resource allocation. To reduce delays, have a front-end developer, artist, go-to-market strategy, and sufficient onboarding time ready. 

## What information do we need to provide to deploy our smart contracts?

To get started, you'll provide our team with:

- Network: (Mainnet or Testnet)
- A testnet/mainnet Ethereum wallet address (that you currently own and control) you'll use to manage your Art Blocks Engine smart contracts.
- The name you’ll use for tokens from your contract (e.g., for Art Blocks, it is "Art Blocks")
- The ticker symbol you’ll use for tokens from your contract (e.g., for Art Blocks, it is "BLOCKS")
- Deployment Type: V3 Onchain Engine or V3 Flex Engine
- Minter Type: set price eth only, set price custom erc20, merkle tree allowlist, holder-gated, linear DA, exponential DA, and exponential DA with settlement
- Starting project ID # (>=0):
- Set `autoApproveArtistSplitProposals` true or false**

**It needs to be set at deployment and cannot be changed later. 

tldr - if true, artist royalty wallet changes are auto-approved. If false, the contract admin will need to approve the artist's royalty wallet changes. This is an added check to ensure your artists aren't changing royalty wallets to a random address, which could complicate accounting/ OFAC compliance. 

We cannot deploy your contract until you provide the above information. **The name and symbol tied to your contract cannot change once your contract is deployed.**

## Does Art Blocks create a front-end site for our project?

No, partners are responsible for creating and designing their customer-facing experience. 

However, we do have a [front-end React template](https://github.com/ArtBlocks/artblocks-engine-react) with web3 functionality you need to launch a minting site. You will still be responsible for designing the user exerpeicne, but this significantly reduces the time needed to complete a front-end. 

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

## Contract Ecosystem

**Core contract:**
This is the smart contract that controls the artwork created by the artist. No financial transactions occur on this smart contract.

**AdminACL:**
By default, Engine smart contracts have two sets of permissions, Admin and Artist. The AdminACL contract controls which wallets can access which functions on your core contract. If you'd like to assign more granular control of your smart contract to different wallets, you can fork and customize the AdminACL contract. 

**Minter Filer:**
The minter filter configures minter-types to specific projects. 

**Minter contract:**
These smart contracts receive funds and split them between the artist(s) and the platform. Artists receive funds directly from these contracts.

## How do we list Art Blocks Engine pieces on secondary markets?

Secondary marketplaces will automatically detect and display projects on your contract. If you’d like each project to have its own storefront on OpenSea, please contact an account manager to facilitate the change. 

## What's the difference between a testnet token and a mainnet token?

**Testnet tokens are free, unlimited, and worthless.** They only exist as a tool for the testing environment before spending actual money (Ether) deploying on Ethereum’s mainnet.

## Flex: What are the limitations around file size and file type for external assets? How many external assets can a project have?

There are no explicit limitations on the contract side, neither for file size or type or how many external assets a project can have. Ultimately, this is at the discretion of the artist, but Art Blocks recommends paying close attention to ensure that artworks are as accessible as possible for as many different types of users as possible. Generally speaking, the above factors should be influenced by trying to achieve the best user experience for the artwork in terms of performance and load time.

Some additional recommendations:

- Try to keep the overall download size for users viewing the work to be under ~10mb OR ensure the artwork description mentions the heavier load/longer loading time. Additionally, consider whether or not it may make sense to have a loading indicator as part of the artwork itself.
- When working with less common file types, remember to test on various platforms/browsers, to ensure the best cross-platform compatibility possible.

## Flex: Can JS external asset dependencies make external calls to other APIs/assets?

Having your JS external asset dependencies making external calls, whether it's to an API or other assets, is not a supported use of the Engine Flex offering, as it breaks the assumption of only utilizing off-chain decentralized platforms. We encourage you to, instead, serialize any data you may need from these external calls into assets (JSON, TXT, etc) that are also stored on the platforms Engine Flex currently supports (IPFS and Arweave).

## For the status of a project on the contract, how does 'active' and 'paused' differ?

The value of `paused` is determined by artist, whereas `active` is determined by contract admin. Both need to be in a mintable state (`paused`=false, `active`=true) for a project to be publicly available to mint.

## Why is there a small delay between the token's mint transaction confirming and it being viewable on the Art Blocks Generator (live view)?

Art Blocks uses the decentralized Graph network to index on-chain data in our publicly available subgraph. There can be a slight delay between the first block confirmation on the ethereum network for a transaction and that transaction being indexed by our subgraph. To mitigate this, as an Art Blocks engine provider, your client should be waiting multiple block confirmations (we recommend at least 2 blocks) before it shows the generator view to the user. The generator will return an error message if the token is not indexed yet, accompanied by 4XX status code. Many clients also employ a polling strategy, only showing the requested generator view once the requested generator url is returning a 2XX status code.

## How does project size work on the minterFilter contract vs Core contract?

A project's max invocations on Art Blocks contracts are handled differently on the Core contract and the minterFilter contract.

On the **Core contract**, setting a project size establishes the project's maximum size, and this value **cannot** be increased once set. The max invocations on the core contract define the absolute upper limit for the number of mints for a specific project.

On the other hand, the **minterFilter contract** allows you to set max invocations for a specific minter using the `manuallyLimitProjectMaxInvocations` function. This setting does not lock the project size but controls the maximum number of mints allowed by that particular minter. When updating the maxInvocations value for a project in the minterFilter contract, you must adhere to these conditions:

1. The new value of _maxInvocations should not be greater than the maxInvocations set in the core contract.
2. The new value of _maxInvocations should not be less than the current number of invocations.

## How does `autoApproveArtistSplitProposals` work?

When `true`, `aproveArtistSplitProposals` is a feature thatallows artists to automatically change their royalty split payout address and the split percentage without requiring approval from the contract admin. This makes the process faster and more convenient for artists but may increase the risk of unauthorized changes to royalty wallets, which could complicate accounting or OFAC compliance. 

If set to `else` the contract admin will need to approve any changes to the artist's royalty wallet, adding a layer of security and control.

## When should I enable GPU rendering?

If your image preview is showing a blank, incomplete, or invalid rendering for a token, turning on GPU rendering may resolve the issue. GPU rendering is managed by the Art Blocks team and enabling is determined on a case-by-case basis. Before requesting GPU rendering, check your project script code for any potential issues and/or try increasing your render delay (up to 10min). Reach out to the Art Blocks team to enable GPU rendering on a specific project if the token issues continue after adjusting the delay.
