---
order: 1000
description: What is Art Blocks Engine and Engine Flex — platform overview, use cases, and contract architecture.
---

# What is Art Blocks Engine?

Art Blocks Engine and Engine Flex are white-label solutions that bring Art Blocks' generative NFT minting technology to third-party platforms. Engine partners own their smart contracts and can release as many generative projects as they want, using the same infrastructure, rendering, and minting tools as Art Blocks flagship.

---

## What Generative Art Is

If you're new to generative art: generative art is created by defining a system (a set of rules) and introducing randomness. Artists write computer algorithms that explore a range of possibilities — each output is unique, but all outputs belong to the same coherent project.

With Art Blocks' on-chain approach:
- The algorithm lives permanently on the blockchain
- Each mint generates a unique token hash
- The hash seeds the algorithm, producing a one-of-a-kind output
- No one — not even the artist — knows exactly what a piece will look like before it's minted

The interesting part is that generative art works in series. Instead of a single artwork, the artist creates a system capable of hundreds or thousands of compelling outputs. Taken as a whole, the project expresses the full range of possibilities within that algorithm.

---

## Engine vs. Engine Flex

Engine Flex is the more capable of the two contract variants — and the one most new Engine deployments use. It supports everything the standard Engine contract supports, plus additional features including PostParams, multiple dependencies, and decentralized storage. A Flex contract can run a completely traditional on-chain generative art project just as well as one using advanced features.

| | Art Blocks Engine | Art Blocks Engine Flex |
|---|---|---|
| **Script storage** | Fully on-chain | Fully on-chain |
| **Dependencies** | Single library from the Dependency Registry | Multiple Dependency Registry entries, IPFS, Arweave, or BytecodeStorage |
| **PostParams** | Not supported | Supported — on-chain configurable parameters collectors can adjust post-mint |
| **Token output** | Deterministic from script + hash | Deterministic from script + hash + any external dependencies + PostParam settings |
| **Best for** | Simple, single-dependency projects | Any project — traditional on-chain, PostParams-enabled, multi-dependency, or decentralized storage |

Both variants use the V3 Engine core contract, are ERC-721 compliant, integrate with the Art Blocks Minter Suite, and are indexed by the Art Blocks subgraph.

---

## How It Works

Each Art Blocks Engine deployment consists of:

- **A V3 Engine or V3 Engine Flex core contract** — stores project scripts, token hashes, and royalty data
- **A shared Minter Suite** — the same minting contracts used by Art Blocks flagship (Dutch Auctions, allowlists, RAM, and more)
- **Integration with Art Blocks rendering infrastructure** — tokens are accessible via the Token API, Generator API, and Media Proxy

When a collector mints:
1. A unique 32-byte hash is generated from the transaction
2. That hash seeds the artist's algorithm, stored on-chain
3. The artwork is rendered deterministically — same hash, same output, always
4. Token ownership is recorded on the ERC-721 contract

The partner owns and controls their contract. Art Blocks provides the infrastructure.

---

## Engine Flex Capabilities

The Flex contract unlocks a range of capabilities beyond the standard Engine contract. A Flex project can use any combination of these — or none at all (a fully on-chain project with a single dependency is equally valid on a Flex contract):

- **PostParams** — On-chain configurable parameters that collectors (or artists) can adjust after minting. Enums, booleans, integers, colors, timestamps, and more. Entirely on-chain — no external storage required. See [PostParams](/protocol/postparams/) for details.
- **Multiple Dependency Registry entries** — Reference more than one library from the Art Blocks Dependency Registry in a single project.
- **IPFS** — Content-addressed files (images, audio, data) pinned on IPFS. Reference using the CID.
- **Arweave** — Permanent decentralized storage. Reference using the Arweave transaction ID.
- **BytecodeStorage** — On-chain byte array storage. Large assets stored directly on Ethereum.

External dependencies (IPFS, Arweave, BytecodeStorage, Dependency Registry) are accessed via the `tokenData.externalAssetDependencies` array in the artist's script. See the [On-Chain Generator](/protocol/on-chain-generator/) page for how FLEX dependencies are structured.

---

## Smart Contract Architecture

Both V3 Engine variants integrate with the following peripheral contracts:

| Contract | Role |
|---|---|
| **Admin ACL** | Manages admin access. Flexible, extensible, upgradable. |
| **Randomizer** | Generates token hashes at mint time. Supports async hash generation. |
| **Core Registry** | Notifies the indexing service when new Engine contracts are deployed. Also registers contracts with the shared minter suite. |
| **MinterFilter** | Coordinates minter assignment. Partners can approve custom minters for their contracts. |

For the full architecture overview with diagrams, see [V3_ARCHITECTURE.md](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/V3_ARCHITECTURE.md).

---

## Use Cases

Engine is used across a wide range of industries:

- **Art galleries and art houses** — launching branded generative collections
- **Media and technology companies** — generative content experiences for audiences
- **Fashion brands** — limited-edition digital collectibles
- **Gaming** — procedural item generation
- **Sports** — fan engagement collectibles
- **Independent platforms** — BYOP ("Build Your Own Platform") generative art infrastructure

Interested? Contact [info@artblocks.io](mailto:info@artblocks.io) to discuss your project.
