---
order: 1100
description: A technical overview of the on-chain generator and introduction to the ecosystem of preservation projects at Art Blocks.
---

# Introducing the On-Chain Generator

*by Ben Yoshiwara*

Art Blocks is excited to announce a new advancement in our commitment to preserving the unique digital artworks created on our platform: the deployment of our on-chain generator contract. This represents a step forward in ensuring the perpetual availability and accessibility of Art Blocks pieces.

Want to see it in action? Check out our [demo repository](https://github.com/ArtBlocks/on-chain-generator-viewer) and [demo site](https://artblocks.io/onchain/generator) to see how easy it is to display Art Blocks works with the on-chain generator!

## Progressing Art Blocks Preservation

In the past, viewing an Art Blocks piece relied on a centralized [generator](https://docs.artblocks.io/creator-docs/art-blocks-101/generator/) to assemble the HTML document that makes up an artwork, combining a project’s script and dependencies. The project's creative code and essential parameters are stored on-chain, and while the artwork can be manually reconstructed by anyone, for convenience Art Blocks has served artworks up with a backend.

This new on-chain generator removes the need for that backend entirely, allowing anyone to retrieve any Art Blocks artwork entirely using just a single call to our smart contract.

We’ve ensured that the complete process of generating viewable Art Blocks pieces is now preserved on-chain. This means that even in the distant future, these artworks can be reconstructed and displayed using only the information stored on the Ethereum blockchain, aligning with Art Blocks’ broader efforts in digital art preservation. While our conventional web server-based generator will remain the primary way to view Art Blocks pieces, this on-chain preservation secures their longevity and accessibility for generations to come.

## Why This Matters

The most commonly used dependencies, **p5js** and **threejs**, are now [stored on-chain](https://docs.artblocks.io/creator-docs/art-blocks-101/on-chain/#summary). This means that approximately 90% of all Art Blocks flagship projects can now be fully constructed from on-chain components, while the remaining 10% identify a preferred CDN for already broadly-distributed npm packages that exist on hundreds of thousands of hard drives around the world.

This advancement represents a significant step in ensuring the long-term preservation of Art Blocks pieces. If our conventional infrastructure were to ever become unavailable, the on-chain generator contract handles the complete assembly automatically, ensuring your artwork can always be reconstructed. As long as the Ethereum blockchain exists, these artworks can be constructed and viewed in a web browser without relying on any centralized infrastructure or implicit knowledge.

## Building the Complete System

Our implementation combines several key components:

- **The Core Contracts**: Store the project's creative code and token-specific data that define each unique artwork.
- **[The Dependency Registry](https://etherscan.io/address/0x37861f95882ACDba2cCD84F5bFc4598e2ECDDdAF#readProxyContract)**: Manages JavaScript library dependencies for projects across supported Art Blocks contracts. Dependencies can be referenced via CDN or stored fully on-chain, allowing for progressive decentralization. We've started by uploading our most widely used dependencies on-chain: **p5.js** (v1.0.0) and **three.js** (v0.124.0), with plans to add more over time.
- **[scripty.sol](https://github.com/intartnft/scripty.sol)**: "A gas-efficient on-chain HTML builder service that's tuned for stitching large JS based tags together." Created by [int.art](#). Big shout out to the int.art team for building **scripty.sol**, which was instrumental in making this project possible!
- **[The Generator Contract](https://etherscan.io/address/0x953D288708bB771F969FCfD9BA0819eF506Ac718#readProxyContract)**: Orchestrates the entire process by combining the project script and token data from the core contracts with the appropriate dependency from the registry, assembling everything into a complete, ready-to-view HTML document using **scripty.sol**. The generator supports both plain text HTML and base64-encoded data URIs for maximum flexibility in how the artworks can be displayed.

## Looking Forward

Art Blocks is dedicated to developing cutting-edge technical solutions for the long-term preservation of artworks released on our platform. Through innovations like the **BytecodeStorage** library, **Dependency Registry**, and **On-Chain Generator**, we are expanding the boundaries of blockchain capabilities and remain committed to pushing these limits further in the future.
