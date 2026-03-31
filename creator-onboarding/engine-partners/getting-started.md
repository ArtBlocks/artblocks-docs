---
order: 900
description: Art Blocks Engine partner onboarding — step-by-step from initial outreach to mainnet launch.
---

# Getting Started as an Engine Partner

An overview of the steps required to onboard as an Art Blocks Engine partner, from initial contact through mainnet deployment and your first project launch.

---

## 1. Initial Outreach

[!badge Timeline: 1–2 weeks]

Reach out to [info@artblocks.io](mailto:info@artblocks.io) to start the conversation. The Art Blocks team will discuss your project goals, explain what's included in an Engine partnership, and align expectations on scope, cost, and timeline.

---

## 2. Project Scope

[!badge Timeline: 1–2 weeks]

The Art Blocks team works with you to define:

- Contract type: V3 Engine or V3 Engine Flex
- Number of minter types needed
- Network: Ethereum, Arbitrum, or Base
- Frontend integration requirements
- Any custom functionality

---

## 3. Contract Agreement

[!badge Timeline: 1 week]

Once scope is agreed, you'll sign Art Blocks' partnership agreement with the operations team.

---

## 4. Smart Contract Details

[!badge Timeline: 1–2 days]

To deploy your contract, provide the Art Blocks team with:

| Field | Notes |
|---|---|
| **Admin wallet address** | The Ethereum wallet you'll use to manage your Engine contracts |
| **Token name** | Name for tokens from your contract (e.g., "Art Blocks" for AB tokens) |
| **Token symbol** | Ticker symbol (e.g., "BLOCKS") |
| **Deployment type** | V3 Engine or V3 Engine Flex |
| **Minter types** | Which minters you need (Set Price ETH, Dutch Auction, Allowlist, etc.) |
| **Starting project ID** | Typically `0` |
| **autoApproveArtistSplitProposals** | `true`: artist royalty changes are auto-approved. `false`: admin must approve each change. Cannot be changed after deployment. |

!!!warning
The token name and symbol are permanent — they cannot be changed after contract deployment.
!!!

---

## 5. Testnet Deployment & Configuration

[!badge Timeline: 1 week]

Art Blocks deploys your contract on Sepolia testnet, configures the initial state, and transfers admin ownership to your wallet. You can begin testing your generative scripts immediately.

Contracts are batched for deployment twice per month.

---

## 6. Testnet Infrastructure Integration

[!badge Timeline: 1 week]

Art Blocks integrates your testnet contract with:

- Rendering infrastructure (Token API, Generator API, Media Proxy)
- Art Blocks staging website access for project configuration via the Creator Dashboard

Your project admin dashboard becomes accessible for project shell creation and artist setup.

---

## 7. Partner Site Integration

[!badge Timeline: Weeks to months, depending on partner]

Your team integrates your frontend with the testnet contract:

- [ ] Connect your frontend to testnet contract addresses
- [ ] Test minting flows (fixed price, Dutch Auction, allowlist, etc.)
- [ ] Test with custom ERC-20 if applicable
- [ ] Request a script audit from Art Blocks
- [ ] Cross-browser test your scripts at [browserstack.com](https://www.browserstack.com/)

---

## 8. Test Mints on Partner Site

[!badge Timeline: Depends on partner]

Run full end-to-end testing on testnet via your frontend:

- [ ] Mint test tokens using all planned minter types
- [ ] Verify token metadata appears correctly via the Token API
- [ ] Test generator URLs render artwork correctly
- [ ] Verify subgraph indexing for your contract
- [ ] Let Art Blocks know when testing is complete and you're ready for mainnet

---

## 9. Mainnet Deployment

[!badge Timeline: 2 weeks]

Art Blocks deploys your mainnet contract and integrates it with production infrastructure.

---

## 10. Mainnet Infrastructure Integration

[!badge Timeline: Depends on partner]

Your team migrates to mainnet:

- [ ] Update frontend to mainnet contract addresses
- [ ] Use the same minting mechanics tested on testnet
- [ ] Verify all integrations with production APIs

---

## 11. Mint Token #0

Your first official token! Mint token #0 via your frontend to confirm the end-to-end flow.

---

## 12. Project Launch

You choose your launch date. Allow at least one week between a successful token #0 and public go-live.

[!badge Timeline: 1 week from token #0]

---

## Setting Up Projects

Once your contract is deployed and infrastructure is integrated, you can create project shells and set up artist projects via the Art Blocks Creator Dashboard at [create.artblocks.io](https://create.artblocks.io/).

The Creator Dashboard supports:
- Project shell creation
- Script upload and preview
- Payment configuration (primary splits, secondary royalties via 0xSplits)
- Minter configuration
- Staging and production environment management

Artists can be onboarded to the Creator Dashboard using their own wallets. The project admin (your Engine admin wallet) handles project activation.

---

## Project Activation and Launch State

Project visibility is controlled by two flags:

| State | Visibility | Purchasable By |
|---|---|---|
| `inactive + paused` (default) | Not visible publicly | No one |
| `active + paused` | Publicly visible | Artist wallet only |
| `active + unpaused` | Open to purchase | Anyone |

**Activation** is typically done by the contract admin. **Unpausing** is done by the artist. For Dutch Auctions, the auction opens automatically at the configured start time once unpaused.

---

## Key Resources

- [Art Blocks Creator Dashboard](https://create.artblocks.io/) — project setup and management
- [Art Blocks Contracts GitHub](https://github.com/ArtBlocks/artblocks-contracts) — full contract source
- [V3 Architecture Overview](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/V3_ARCHITECTURE.md) — architecture diagrams
- [Minter Suite Documentation](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/MINTER_SUITE.md)
- [Token API](/developer/token-and-generator-apis/) — integration endpoints
- [GraphQL Reference](/developer/graphql/) — querying project and token data
