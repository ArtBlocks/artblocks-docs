# Minter Suite Overview

The Art Blocks Shared Minter Suite is a collection of smart contracts that enable artists to choose how they distribute their project's tokens to collectors. It is used by all Art Blocks Studio and Engine projects on V3 contracts.

---

## Core Principles

### Transparency

All minter smart contracts have verified source code and are developed publicly in the [artblocks-contracts repository](https://github.com/ArtBlocks/artblocks-contracts). Artists and collectors can inspect exactly what rules govern a mint before participating.

### Decentralized & Trust-Minimized

Minting runs on immutable, on-chain smart contracts. Art Blocks and artists have specific, documented privileges (e.g., configuring auction parameters) but minter contracts are designed to minimize those privileges and align incentives between all parties.

### Non-Custodial

Minting is a transaction between the collector and the minter smart contract — the contract handles pricing, settlement, and fund custody. No centralized party holds collector funds during an active auction.

### Honest

Art Blocks does not implement restrictions that appear to improve fairness but don't work in practice. See [What Doesn't Work](#what-doesnt-work) below.

---

## Architecture

### Mix-and-Match

Artists can assign different minters for different phases of a project. For example:

1. Use an allowlist minter for early-access minting
2. Switch to a Dutch Auction with Settlement for public sale

Each minter supports capping to a maximum number of invocations. Minter A might be used for the first 200 tokens, then minter B takes over for the remainder.

### MinterFilter

The `MinterFilter` contract is the coordination layer:

- Maintains a list of globally approved minters
- Assigns a specific minter to each project (set by the artist or admin)
- Validates that a minter is the approved minter for a project before allowing a token to be minted
- Ensures the project is on a registered Engine contract

### Minters

Each minter handles:

- The token purchase process (`purchase` and `purchaseTo` functions)
- Maximum invocations for the minter (can be lower than project max)
- Pricing: price in wei, currency symbol, currency address
- Minter type metadata

For the full architecture overview, see [MINTER_SUITE.md](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/MINTER_SUITE.md) in the contracts repository.

---

## Fairness Framework

Different minting approaches achieve different kinds of fairness. Artists should choose a minter that aligns with their project's goals and audience.

### Capitalist Fairness

Those willing to pay the most can participate. Dutch Auctions achieve this by starting at a high price and decreasing until collectors buy in.

### Insider Fairness

Pre-approved community members get priority access. Allowlist minters achieve this — only wallets on a pre-configured list can mint, optionally limited to a set number per wallet.

### Equal-Chance Fairness

All collectors have roughly equal odds. This is theoretically desirable but difficult to achieve on Ethereum, where bots can submit many transactions simultaneously. Art Blocks provides tools (like RAM and Dutch Auctions with Settlement) that reduce bot advantage without hidden mechanisms.

---

## What Doesn't Work

Art Blocks does not implement certain restrictions that appear to improve fairness but are ineffective in practice:

**One mint per wallet** — Bots trivially create many wallets. This restriction disadvantages human collectors more than bots, and can create a false impression of healthy distribution.

**No minting from smart contracts** — Bots mint from EOAs (externally owned accounts). This rule is also harmful to collectors using multi-sig wallets for security.

**One mint per transaction** — Bots submit many transactions. This rule mainly adds gas costs and disadvantages collectors who want to mint from multi-sig wallets.

**Low, fixed prices** — For highly-anticipated projects, low fixed prices strongly favor bots. Consider Dutch Auctions or allowlists for high-demand drops.

---

## Available Minters

See the [Minters catalog](/developer/minter-suite/minters/) for a complete reference of all available minter types with their key parameters and use cases.
