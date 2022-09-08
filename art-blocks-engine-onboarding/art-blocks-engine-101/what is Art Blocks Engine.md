# What is Art Blocks Engine and Engine Flex?
Art Blocks Engine and Engine Flex are custom branded solutions from Art Blocks. Our offerings allow the generative NFT minting technology used by artists at Art Blocks to be integrated with third-party sites. 

Engine allows partners to release generative outputs using our existing smart contracts and rendering infrastructure resulting in turnkey and branded generative projects. Engine partners own their smart contracts and can use them to release as many projects as they like as often as they like.

We currently partner with organizations from every sector that are interested in launching generative collections, but are particularly interested in the fashion, sports, media, manufacturing, and fine art industries.

For more information on Art Blocks Engine partnerships please contact: info@artblocks.io

## What is the difference Art Blocks Engine and Engine Flex?

Art Blocks Engine is our offering that aligns most closely with the Art Blocks flagship product (https://artblocks.io), and has the same technical approach to on-chain art where artists store the entirety of their generative algorithms on-chain within the Engine smart contract and are limited to a single, widely-distributed, off-chain dependency (e.g. p5js).

With Art Blocks Engine Flex artists are able to include off-chain assets, stored on the decentralized storage solutions of IPFS or Arweave, as additional inputs into their creative coding practice. This allows for example a project that takes an image as an input and creates 1of1ofX outputs applying a generative practice to this input image–combining a generative script, a token hash, and additional off-chain assets.

## How does Art Blocks Engine Flex work?

With Art Blocks Engine Flex contracts, a per-project (as opposed to per-contract) field is available on all projects that allows an artist to set a single off-chain dependency or set of off-chain dependencies based on the content ID locations where these dependencies are stored on IPFS or Arweave.

Currently, we do not yet support the turnkey ability to programically upload/pin these dependencies to IPFS/Arweave within the Engine experience directly; however, our team is more than happy to assist partners in the process of uploading/pinning assets on IPFS/Arweave using existing third party solutions for doing so (e.g. Pinata in the case of IPFS).

Note that for a single project, it is possible to have a single off-chain dependency (e.g. a single image file) or a set of off-chain dependencies (e.g. a series of images from a set). This means that is possible for example to have a project that creates 1of1ofN generative variants of a single base image asset, or one in which for a given token a random image is selected from the base image asset set, and then a generative process is applied to it. 

It is also important to note that images are not the only supported external asset dependency type. It is possible to reference any file type that can be pinned/uploaded to IPFS or Arweave and intelligbly incorporated into a generative algorithm to create interesting artistic outputs. For example, a project could use `tensorflow.js` as its single-depedency, have its generative script be a tensorflow based creative coding algorithm, and store the model file for the machine learning model on IPFS or Arweave to support a ML/AI based project.

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
