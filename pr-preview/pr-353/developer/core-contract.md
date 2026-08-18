# Core Contract (V3)

The Art Blocks V3 Core Contract is the open-source ERC-721 smart contract that powers Art Blocks projects. All projects — Studio, Curated, and Engine — run on this contract. It manages token ownership, project scripts, token hashes, and royalty configuration.

The full source code is available in the [artblocks-contracts GitHub repository](https://github.com/ArtBlocks/artblocks-contracts).

---

## Variants

The V3 Core Contract comes in two variants:

### V3 Engine

The fully on-chain variant. An artist's generative script lives entirely on the blockchain. Projects may reference a single external dependency (a JavaScript library) via the [Art Blocks Dependency Registry](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/README.md#dependencyregistry) — many of which are themselves stored fully on-chain (p5.js v1.0.0, Three.js v0.124.0).

This is the highest-durability option: the token can always be reconstructed from on-chain data alone.

### V3 Engine Flex

Extends V3 Engine with support for external asset dependencies. Projects can reference assets stored on:

- **IPFS** — content-addressed, decentralized storage
- **Arweave** — permanent decentralized storage
- **BytecodeStorage** — on-chain byte array storage for large assets
- **Art Blocks Dependency Registry** — registered on-chain library assets

Flex is appropriate when a project requires assets too large to store efficiently on-chain (images, ML models, audio, large datasets). The generative script itself still lives on-chain.

For details on how Flex dependencies are structured and accessed in scripts, see the [On-Chain Generator](/protocol/on-chain-generator/) page.

---

## Contract Architecture

Each V3 Engine deployment integrates with the following peripheral contracts:

| Contract | Role |
|---|---|
| **Admin Access Control List (ACL)** | Manages admin access grants to the core contract and related contracts. Highly flexible and upgradable. |
| **Randomizer** | Generates pseudo-random hashes when tokens are minted. Architecture supports async or custom hash generation. |
| **Core Registry** | Notifies the subgraph indexing service when a new Engine contract is deployed, making it queryable. Also registers the contract with the shared minter suite. |
| **Minter Suite** | Collection of minting contracts. See [Minter Suite](/developer/minter-suite/overview/) for details. |

The [V3 Architecture Overview](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/V3_ARCHITECTURE.md) in the contracts repository includes architecture diagrams.

---

## ERC-2981 Royalties

All V3.2+ contracts (all Studio contracts, and Engine contracts deployed after May 2024) conform to the [ERC-2981](https://eips.ethereum.org/EIPS/eip-2981) royalty standard.

!!!info
All versions of Art Blocks core contracts integrate with the [Royalty Registry](https://royaltyregistry.xyz/lookup), which is supported by all major secondary marketplaces.
!!!

ERC-2981 requires royalty payments to route to a single address. Art Blocks contracts integrate with [0xSplits](https://splits.org/) to distribute royalties to multiple parties (artist, additional payee, platform) through a single, permissionless, immutable splitter contract.

### How It Works

When payment information is configured in the Creator Dashboard, the V3.2+ contract automatically deploys a 0xSplits splitter contract for the project. This splitter:

- Receives all secondary royalty payments
- Distributes funds according to configured splits (artist share, additional payee share, Art Blocks share)
- Is immutable once deployed — to change splits, a new splitter must be deployed

Artists can view their current splitter address in the Creator Dashboard. Funds can be viewed and withdrawn at [app.splits.org](https://app.splits.org).

### Royalty Distribution

For Art Blocks Studio projects:
- **Primary sales**: 90% to artist, 10% to Art Blocks
- **Secondary royalties**: Up to 5% total (honored by major marketplaces). By default, split 2/3 to artist and 1/3 to Art Blocks.

Artists set their preferred royalty percentage and any additional payee splits in the Payments section of the Creator Dashboard.

### Updating Splits

Splitter contracts are immutable. To update a secondary royalty split:

- Email [royalties@artblocks.io](mailto:royalties@artblocks.io) or post in `#artist-general` on Discord
- Art Blocks will deploy a replacement splitter and handle marketplace updates

For non-US artists, Art Blocks will request a W8BEN or W8BENE form before distributing royalties.

---

## Key Contract Functions

The following functions are commonly referenced by integrators and dashboard tools:

| Function | Description |
|---|---|
| `projectDetails(projectId)` | Returns project name, artist, description, website, license |
| `projectScriptInfo(projectId)` | Returns script type, count, and dependency info |
| `projectScriptByIndex(projectId, index)` | Returns a script segment (scripts >24KB are split into segments) |
| `showTokenHashes(tokenId)` | Returns the hash for a given token ID |
| `addProject(...)` | Creates a new project shell (admin only) |
| `updateProjectSecondaryMarketRoyaltyPercentage(...)` | Sets artist royalty percentage (artist only) |

For a full function reference, see the contract source on [Etherscan](https://etherscan.io/) or in the [GitHub repository](https://github.com/ArtBlocks/artblocks-contracts).

---

## Token ID Structure

Art Blocks token IDs encode both the project and the invocation number:

```
tokenId = (projectId × 1,000,000) + invocationNumber
```

For example, token `78000042` is invocation #42 from project #78.

To decode in JavaScript:

```javascript
const tokenId = parseInt(tokenData.tokenId)
const projectId = Math.floor(tokenId / 1_000_000)
const invocationNumber = tokenId % 1_000_000
```

---

## Additional Resources

- [Art Blocks Contracts GitHub Repository](https://github.com/ArtBlocks/artblocks-contracts) — full source code, deployment scripts, documentation
- [V3 Architecture Overview](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/V3_ARCHITECTURE.md) — architectural diagrams and design rationale
- [Minter Suite Documentation](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/MINTER_SUITE.md) — minter suite architecture
- [Dependency Registry](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/README.md#dependencyregistry) — on-chain library registry
