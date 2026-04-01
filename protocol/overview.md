---
order: 1000
icon: telescope
label: Overview
---

# Art Blocks Protocol Overview

Art Blocks is built on a simple but radical premise: **the algorithm is the artwork**. Every generative art project on Art Blocks stores its creative code permanently on a blockchain, and every token produced by that code lives there too — deterministic, immutable, and accessible to anyone with a web browser, forever.

This page explains the philosophy behind Art Blocks' on-chain architecture and the key technologies that make it work.

---

## Why On-Chain?

Most NFTs store only a pointer to off-chain data — an image on a server, a file on IPFS pinned by a single party. When the server goes down or the pinning lapses, the NFT becomes a record of ownership for something that no longer exists.

Art Blocks takes a different approach. Every project's generative script, its dependency libraries, and the hashes that seed each token's unique output are stored directly on the Ethereum blockchain. The artwork cannot be changed, taken down, or lost — as long as Ethereum exists, every Art Blocks token can be reconstructed from first principles.

This is a meaningful guarantee for both artists and collectors:

- **Artists** know their work will outlast any company, server, or service — including Art Blocks itself.
- **Collectors** know their token is a permanent record, not a receipt for something that might disappear.

---

## How Generative Art Works On-Chain

Every Art Blocks project is a JavaScript algorithm (the "script") stored on a smart contract. When a collector mints a token:

1. The blockchain generates a unique 32-byte hash — a random seed created from the transaction data.
2. That hash is injected into the artist's script as `tokenData.hash`.
3. The script runs deterministically: the same hash always produces the same visual output.
4. The resulting artwork is assembled and rendered by the [Art Blocks Generator](/protocol/on-chain-generator/).

The token itself is an ERC-721 NFT. Its metadata — script, hash, artist address, royalty configuration — lives entirely on the contract.

---

## Key Technologies

### The On-Chain Generator

The [Art Blocks On-Chain Generator](/protocol/on-chain-generator/) is a smart contract that assembles a complete, browser-viewable HTML document from on-chain data alone. It retrieves the project script, the token hash, and any dependency libraries from the blockchain, combines them using [scripty.sol](https://github.com/intartnft/scripty.sol), and returns a fully self-contained HTML page that renders the artwork.

This means any Art Blocks token can be reproduced with a single call to a smart contract — no Art Blocks servers required.

### The Dependency Registry

The [Art Blocks Dependency Registry](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/README.md#dependencyregistry) is a fully on-chain software registry that stores JavaScript library releases on the blockchain. p5.js v1.0.0 and Three.js v0.124.0 — used by the vast majority of Art Blocks flagship projects — are fully on-chain, ensuring those projects can always generate their outputs without relying on any CDN.

For projects using other approved library versions, the registry records a preferred CDN and the hash of the release, pointing to widely-distributed packages present on hundreds of thousands of developer machines worldwide.

### Engine Flex

[Art Blocks Engine Flex](/creator-onboarding/engine-partners/what-is-engine/) is the more capable Engine contract variant. It supports everything a standard Engine contract does, and additionally enables PostParams, multiple Dependency Registry entries, IPFS/Arweave decentralized storage, and on-chain BytecodeStorage — in any combination. A Flex contract can run a fully on-chain traditional project or a project using any of these advanced features. Most new Engine deployments use Flex.

### PostParams

[PostParams](/protocol/postparams/) (Post-Mint Parameters) allow token owners and artists to set configurable on-chain values after minting — changing color palettes, animation parameters, or any other dimension the artist exposes. Parameters can be locked at artist-configured dates to cement values permanently. PostParams make it possible to create artworks that evolve, respond to their collectors, or bridge the digital and physical worlds.

---

## The Core Contract

All of this runs on the [Art Blocks V3 Core Contract](/developer/core-contract/) — an open-source ERC-721 contract available in two variants:

- **V3 Engine** — fully on-chain storage; the script and all metadata live on the blockchain.
- **V3 Engine Flex** — extends V3 Engine with optional capabilities: PostParams, multiple Dependency Registry entries, IPFS/Arweave decentralized storage, and BytecodeStorage. Traditional on-chain projects are equally valid on a Flex contract.

Both variants integrate with the shared [Minter Suite](/developer/minter-suite/overview/) and expose the same APIs to integrators.

---

## Developer Reference

For technical implementation details, see:

- [On-Chain Storage](/protocol/on-chain-storage/) — NFT metadata storage comparison and Art Blocks' approach
- [On-Chain Generator](/protocol/on-chain-generator/) — How the generator assembles tokens from blockchain data
- [PostParams](/protocol/postparams/) — Configurable on-chain parameters for evolving artworks
- [Developer Reference](/developer/) — Core contract, APIs, GraphQL, MCP Server, and Minter Suite
