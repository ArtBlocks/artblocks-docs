---
order: 1000
---
# What is Art Blocks Engine and Engine Flex?
Art Blocks Engine and Engine Flex are custom branded solutions from Art Blocks. Our offerings allow the generative NFT minting technology used by artists at Art Blocks to be integrated with third-party sites.

Engine allows partners to release generative outputs using our existing smart contracts and rendering infrastructure resulting in turnkey and branded generative projects. Engine partners own their smart contracts and can use them to release as many projects as they like as often as they like.

We currently partner with organizations from every sector that are interested in launching generative collections, but are particularly interested in the fashion, sports, media, manufacturing, and fine art industries.

For more information on Art Blocks Engine partnerships please contact: info@artblocks.io

## What is the difference between Art Blocks Engine and Engine Flex?

Art Blocks Engine is our offering that aligns most closely with the Art Blocks flagship product (https://artblocks.io), and has the same technical approach to on-chain art where artists store the entirety of their generative algorithms on-chain within the Engine smart contract and are limited to a single, widely-distributed, off-chain dependency (e.g. p5js).

With Art Blocks Engine Flex artists are able to include off-chain assets, stored on the decentralized storage solutions of IPFS or Arweave, as additional inputs into their creative coding practice. This allows, for example, a project that takes an image as an input and creates 1of1ofX outputs applying a generative practice to this input image. This final output combines a generative script, a token hash, and additional off-chain assets.

## How does Art Blocks Engine Flex work?

With Art Blocks Engine Flex contracts, a per-project (as opposed to per-contract) field is available on all projects that allows an artist to set a single off-chain dependency or set of multiple off-chain dependencies based on the content ID locations where these dependencies are stored on IPFS or Arweave.

Currently, we do not yet support the turnkey ability to programically upload/pin these dependencies to IPFS/Arweave within the Engine experience directly; however, our team is more than happy to assist partners in the process of uploading/pinning assets on IPFS/Arweave using existing third party solutions for doing so (e.g. Pinata in the case of IPFS).

Note that for a single project, it is possible to have a single off-chain dependency (e.g. a single image file) or a set of off-chain dependencies (e.g. a series of images from a set). This means that is possible, for example, to have a project that creates 1of1ofX generative variants of a single base image asset, or one in which for a given token a random image is selected from the base image asset set, and then a generative process is applied to it.

It is also important to note that images are not the only supported external asset dependency type. It is possible to reference any file type that can be pinned/uploaded to IPFS or Arweave and intelligbly incorporated into a generative algorithm to create interesting artistic outputs. For example, a project could use `tensorflow.js` as its single-depedency, have its generative script be a tensorflow based creative coding algorithm, and store the model file for the machine learning model on IPFS or Arweave to support a ML/AI based project.

## What is the smart contract architecture for Art Blocks Engine?

The Art Blocks Engine offers two core contract options: the V3 Engine core contract and the V3 Engine Flex core contract. These contracts are mutually exclusive, and partners should select the appropriate core contract based on their needs and whether they require the flex capabilities.

The V3 Engine core contract is an ERC-721 NFT contract that manages metadata for all Art Blocks NFTs, including artist scripts, token hashes, and token royalty data.

The V3 Engine Flex core contract includes everything in the V3 Engine contract, but also allows artists to use external assets in their Engine tokens. These external assets can be images, videos, audio, or other data and may be stored on decentralized storage systems such as IPFS, Arweave, or on the Ethereum blockchain

Both core contracts integrate with various peripheral contracts to provide flexible, customizable, and extensible functionality. These peripheral contracts are:

- Admin Access Control List (ACL) contract: Manages granting admin access to the core contract and related contracts. It is designed to be highly flexible, extensible, and upgradable.
- Randomizer contract: Generates pseudo-random numbers for the core contract when new tokens are minted. This architecture is designed to be highly flexible, enabling designs that may desire asynchronous random number generation or other hash generation methods.
- Engine Registry contract: Notifies the subgraph indexing service of new Art Blocks Engine tokens. When the Engine Registry emits an event, the subgraph indexing service is notified, and the Engine contract is indexed and made available for querying on the Art Blocks subgraph.
- Minter Suite contracts: A collection of contracts used to mint Art Blocks Engine tokens. The Minter Suite is designed to be highly flexible and can be used to mint tokens in various ways.

Partners should choose between the V3 Engine core contract and the V3 Engine Flex core contract based on their project's goals and technical capabilities. The smart contract architecture for Art Blocks Engine provides a robust and flexible system for managing and creating generative NFTs while integrating with various peripheral contracts to extend its capabilities.

For additional context, please check out [this architecture overview (with accompanying diagrams)](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/V3_ARCHITECTURE.md).

## What is the "minter suite"?

The Art Blocks minter suite is a collection of smart contracts that facilitate the secure and efficient minting of generative art tokens for Engine contracts in the V3 architecture.

A summary of the division of responsibilities between the MinterFilter and individual Minters can be summarized as:

- MinterFilter:
  - Maintains a list of approved minters that can mint tokens for projects on the platform.
  - Assigns a specific minter to each project, which can be updated by the project's artist or the platform's Admin ACL.
  - Checks if the minter is the assigned minter for a project before allowing the token to be minted.

- Minters:
  - Provides information about the minter type and associated core contract and MinterFilter addresses.
  - Handles the token purchase process through the "purchase" and "purchaseTo" functions for specific projects.
  - Managed the maximum number of invocations (for the given minter) for each project.
  - Retrieves price information for tokens in a project, including token price in wei, currency symbol, and currency address.

tl;dr: The MinterFilter serves as a control layer that ensures the correct minter is used for each project, while Minters handle token purchase processes and project-specific settings. This division of responsibilities enables a secure, efficient, and flexible set of contracts that we call the "minter suite".

For additional context, please check out [this architecture overview (with accompanying diagrams)](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/MINTER_SUITE.md).

## What is generative art?

Generative art is about developing systems that define rules for creating art. By introducing randomness to those systems, core concepts are expressed through unique outputs. In a contemporary sense, this means writing computer algorithms to define the system and introduce randomness, which allows for conceptual exploration and rapid iteration.

Creative coders write scripts with specific parameters that introduce and explore features, which generate the final outputs in a collection. With Art Blocks’ generative minting technology, collectors participate in the creation of the art. No one knows exactly what a piece will look like before it's minted, not even the artist. Each NFT is generated at the time of purchase using the buyer’s unique transaction hash to create a ‘1 of 1 of X’, which adds an extra layer of magic as the creator and collector watch a project come alive.

The interesting part of modern generative art is that it involves working in series - often a large series. So instead of pursuing a single compelling work of art, a generative artist creates an algorithm capable of tens, hundreds, or thousands of compelling works of art. Which, when taken as a whole, expresses the range of possibilities contained in a single algorithm.

## What are NFTs?
Nonfungible tokens (NFT) are unique digital assets stored on blockchain technology that can represent any digital or physical asset.

## On-chain vs. off-chain
Art Blocks Engine enables creators to immutably store their generative NFT directly on the Ethereum blockchain (on-chain) or reference an external library or asset (off-chain). For an off-chain implimentation, partners can reference external off-chain assets using decentralized storage solutions like IPFS.

Decentralized and fully on-chain content is the most durable digital asset available. Typically, a creative coder writes a generative script in JavaScript and stores it directly on the blockchain. As long as you have access to a computer, a web browser, and Ethereum’s public ledger, you’ll always be able to reproduce the NFT in its original form and track ownership since creation. An on-chain NFT inherits the provenance, security, and durability of Ethereum itself, making them the highest quality digital asset available.

So, if Art Blocks ever shut down, all on-chain work would still be accessible since it's stored on the decentralized Ethereum blockchain and able to be viewed, bought, sold, and transferred without involving Art Blocks at all.

In contrast, if we store generative algorithms on an Art Blocks-owned database, the NFTs would rely on Art Blocks to return the assets - and if we go offline, the assets would not be retrievable. Similarly, if a script is stored on-chain but uses data from off-chain sources, it's vulnerable to the host of that off-chain data going offline.

Off-chain NFTs rely on assets stored on external servers. There are many reasons to reference off-chain assets - data storage is expensive on Ethereum, and using external assets can reduce the cost of putting data on-chain. It also allows for interesting applications of generative art using external assets. However, if your NFT references external sources and those sources go offline, the NFT will only track ownership of unretrievable data.

For this reason, we only allow certain external libraries to be used in project scripts given their general recognition as extremely reliable file storage sources.

Art Blocks Engine offers on-chain and off-chain solutions with our generative NFT minting technology. Which one is right for you depends on your project’s goals and technical capabilities.

## Creating durable digital assets
Creating on-chain generative NFTs ensures your collectors can expect their digital assets to stay the same forever. But if you choose to launch a generative project with off-chain assets, there are ways to mitigate the risk of going off-line using technology like IPFS or Arweave. We’re happy to chat about the right Art Blocks Engine implementation for your next project.

## Potential use-cases
The landscape of on-demand generative content has plenty of room to experiment. Some of our current partners include artists, galleries, art houses, online publications, and game developers. If you’re exploring an interesting project, get in touch, and let’s build together.

Current and upcoming use cases:

- Fashion
- Premier Artists
- Media / Tech / Consumer brands
- Gaming
- Sports
- BYOP - build your own platform
