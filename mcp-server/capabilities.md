---
order: 800
description: Tools, resources, and example questions for the Art Blocks MCP Server.
---

# Capabilities

The Art Blocks MCP Server exposes **21 tools** and **2 resources** organized into the categories below. Tools are callable by any connected AI agent; resources provide background context that agents can read automatically.

---

## Quick Reference

| I want to... | Use |
|---|---|
| Browse or search projects | `discover_projects` |
| See what's minting now | `discover_live_mints` |
| See what's launching soon | `discover_upcoming_releases` |
| Get full details on a project | `get_project` |
| Look up an artist | `get_artist` |
| Inspect a specific token | `get_token_metadata` |
| View a collector's portfolio | `get_wallet_summary` → `get_wallet_tokens` |
| Mint a token | `get_project_minter_config` → `check_allowlist_eligibility` → `build_purchase_transaction` |
| Update post-mint parameters | `discover_postparams` → `build_configure_postparams_transaction` |
| Scaffold a new art project | `scaffold_artblocks_project` |
| Run a custom data query | `explore_table` → `build_query` → `graphql_query` |

---

## Discovery

Browse, search, and filter Art Blocks projects across all supported chains.

| Tool | What it does | Example question |
|------|-------------|-----------------|
| `discover_projects` | Search and browse the project catalog with filters for text, artist, vertical, chain, tag, floor price, and mintability | "Show me animated Curated projects under 1 ETH" |
| `discover_live_mints` | Find projects currently open for minting (active, unpaused, supply remaining) | "What can I mint right now?" |
| `discover_upcoming_releases` | See projects scheduled to launch in the future | "What Art Blocks projects are dropping this week?" |
| `get_project` | Full details on a specific project — description, trait distribution with rarity percentages, minting config, tags, and artblocks.io link | "Tell me about Fidenza" |
| `get_artist` | Look up an artist by name, profile slug, or wallet address and see all their projects | "What has Tyler Hobbs released?" |
| `list_tags` | List all available tags for filtering (ab500, animated, interactive, curated series, etc.) | "What tags can I filter by?" |

---

## Tokens and Portfolios

Explore individual tokens and collector portfolios. All portfolio tools accept wallet addresses, ENS names, or Art Blocks usernames — and automatically aggregate across all wallets linked to a profile.

| Tool | What it does | Example question |
|------|-------------|-----------------|
| `get_token_metadata` | Rich metadata for a single token — hash, traits, media URLs, live view URL, listing info, owner, and project context | "Show me token #42 from Chromie Squiggle" |
| `get_wallet_summary` | Portfolio overview — total tokens, unique projects, chain distribution, and per-project breakdown | "What does vitalik.eth collect on Art Blocks?" |
| `get_wallet_tokens` | List individual tokens owned by a collector with traits, media, and listing info | "Show me all Art Blocks tokens owned by snowfro" |

---

## Minting and Eligibility

Check pricing, verify eligibility for gated mints, and build unsigned mint transactions.

| Tool | What it does | Example question |
|------|-------------|-----------------|
| `get_project_minter_config` | Minter type, current price, currency, auction timing, remaining supply, and allowlist details | "How much does it cost to mint this project?" |
| `check_allowlist_eligibility` | Check if a wallet/ENS/username is eligible for Merkle allowlist or holder-gated mints — checks all linked wallets when a profile exists | "Am I eligible to mint this project?" |
| `build_purchase_transaction` | Build an unsigned ETH transaction for set-price mints (MinterSetPriceV5). Supports `purchaseTo` for gifting. | "Build a transaction to mint from project X" |

---

## Post-Mint Parameters (PostParams)

Some Art Blocks projects have on-chain configurable parameters that token owners or artists can update after minting.

| Tool | What it does | Example question |
|------|-------------|-----------------|
| `discover_postparams` | Discover available PostParam keys, types, value constraints, authorization rules, and current values for a token | "What parameters can I change on my token?" |
| `build_configure_postparams_transaction` | Build an unsigned transaction to update PostParam values on a token | "Set my token's color to #FF0000" |

---

## Creator Tools

Tools for artists building generative art projects on Art Blocks.

| Tool | What it does | Example question |
|------|-------------|-----------------|
| `scaffold_artblocks_project` | Generate a ready-to-run project scaffold (index.html + art script) for vanilla JS, p5.js, or Three.js with optional FLEX dependencies, PostParams, and `window.$features` stubs | "Scaffold a p5.js Art Blocks project with traits" |

---

## Advanced GraphQL

Six tools for custom queries against the Art Blocks Hasura GraphQL API. Most users will never need these — the tools above cover common use cases. See the [Advanced GraphQL](/mcp-server/advanced-graphql/) page for details.

| Tool | What it does |
|------|-------------|
| `explore_table` | Inspect a table's fields, types, and relationships (curated shortlist or full schema) |
| `validate_fields` | Check whether specific fields exist on a table before writing a query |
| `build_query` | Build a validated GraphQL query with field checks, WHERE filters, and suggestions |
| `query_optimizer` | Rewrite a query to use preferred `*_metadata` tables |
| `graphql_query` | Execute a raw GraphQL query against the Art Blocks Hasura endpoint |
| `graphql_introspection` | Full GraphQL schema introspection |

---

## Resources

Resources provide background context that agents can read automatically to understand the Art Blocks platform.

| Resource URI | Name | Description |
|-------------|------|-------------|
| `artblocks://about` | About Art Blocks | Platform overview, vocabulary (projects, tokens, invocations, hashes), verticals, supported chains, tags, and a guide to which tool handles what. Agents should read this first. |
| `artblocks://generator-spec` | Generator Specification | Authoritative reference for building Art Blocks projects: `tokenData` structure, hash-based PRNG, FLEX dependency types, PostParams, HTML structure, `window.$features`, and a step-by-step script conversion guide. |

---

## Supported Chains

| Chain | Chain ID | Notes |
|-------|----------|-------|
| Ethereum | `1` | Primary chain. Most historical projects live here. |
| Arbitrum One | `42161` | L2 with lower gas fees. Active for newer releases. |
| Base | `8453` | L2 chain. Growing catalog. |

All discovery, metadata, and minting tools support filtering by chain. The default is Ethereum (`1`) when no chain is specified.

---

## Example Conversations

These show how tools chain together for multi-step workflows.

### "I want to find abstract generative art under 0.5 ETH"

1. Agent calls `discover_projects` with `maxFloorPrice: 0.5`, `sortBy: "floor_asc"`
2. Returns matching projects with names, artists, floor prices, and artblocks.io links

### "Check if I can mint Project X and build the transaction"

1. Agent calls `get_project_minter_config` to check the minter type and price
2. Agent calls `check_allowlist_eligibility` if the minter is gated
3. If eligible, agent calls `build_purchase_transaction` to produce the unsigned transaction
4. Agent surfaces any warnings (paused, sold out) before the user signs

### "Show me Tyler Hobbs' work and the traits of Fidenza #100"

1. Agent calls `get_artist` with `artistName: "Tyler Hobbs"` to see all projects
2. Agent calls `get_token_metadata` with the Fidenza token ID to get traits, rarity, media, and live view URL

### "Help me build an Art Blocks project in p5.js"

1. Agent reads `artblocks://generator-spec` for the full specification
2. Agent calls `scaffold_artblocks_project` with `scriptType: "p5js"` and desired flags
3. Agent walks through the generated scaffold and helps customize the art script
