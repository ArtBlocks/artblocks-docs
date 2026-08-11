# Minters

A complete reference of all available minter types in the Art Blocks Shared Minter Suite.

## Quick Reference

| Minter | Use Case | Price Discovery | Bot Resistance |
|--------|----------|-----------------|----------------|
| Set Price – ETH | Simple fixed-price sale | None | Low |
| Set Price – Allowlist | Fixed price, curated audience | None | High (allowlisted only) |
| Set Price – Token Holder | Fixed price, holder-gated | None | Medium |
| Set Price – ERC20 | Custom token payment | None | Low |
| Dutch Auction (w/ Settlement) | Fair price discovery, equalized price | High | High |
| Dutch Auction (exponential) | Price discovery, variable final price | Medium | Medium |
| Dutch Auction (linear) | Price discovery, variable final price | Medium | Medium |
| Dutch Auction + Token Holder | Holder-gated dutch auction | Medium | High |
| Ranked Auction (RAM) | Bid-based, all pay lowest winning bid | High | High |
| Serial English Auction (SEA) | Sequential per-token auctions | High | High |
| Minimum Price | Near-free distribution with small fee | None | Low |
| Minimum Price – Allowlist | Near-free, allowlisted | None | High |
| Polyptych | Identical-hash multi-piece sets | N/A | N/A |

---

## Set Price Minters

### `Set Price – ETH`

The simplest minter. All tokens sell at a fixed price in ETH, first-come-first-served.

**Best for:** Projects with moderate demand, straightforward drops.

**Key parameters:**
- `price`: Price per token in wei
- `maxInvocations` (optional): Minter-level cap on total mints

---

### `Set Price – ETH, allowlisted users only`

Fixed price restricted to an allowlist. Artists configure a list of eligible wallet addresses and optionally limit how many times each address can mint.

**Best for:** Early access passes, community-exclusive drops, token-gated experiences.

**Key parameters:**
- `price`: Price per token in wei
- `merkleRoot`: Merkle root of the allowlist
- `maxInvocationsPerAddress`: Max mints per allowlisted wallet

---

### `Set Price – ETH, token holders only`

Fixed price restricted to holders of a specified ERC-721 token collection.

**Best for:** Rewarding existing community holders; companion piece drops.

**Key parameters:**
- `price`: Price per token in wei
- `holderContract`: Address of the ERC-721 contract holders must own

---

### `Set Price – custom ERC20`

Fixed price accepting any ERC-20 token. Useful for "mint pass" mechanics or custom community tokens.

**Key parameters:**
- `price`: Price in ERC-20 token units
- `currencyAddress`: ERC-20 contract address
- `currencySymbol`: Display symbol

---

## Dutch Auction Minters

### `Dutch Auction (w/ Settlement) – exponential price decrease`

All collectors pay the same final price — the price at which the last token sold. Collectors who purchase above the final price can claim a settlement (refund of the difference). Funds are held non-custodially by the contract until revenues are collected by the artist.

This is the most equitable Dutch auction for buyers: early purchasers aren't penalized for enthusiasm.

**Best for:** High-demand projects where fair price discovery and collector equitability are priorities.

**Key parameters:**
- `startPrice`: Starting price in wei
- `basePrice`: Minimum (resting) price in wei
- `startTime`: Auction start timestamp
- `halfLifeSeconds`: Controls price decay speed (exponential curve)

!!!info
If an artist reduces max supply mid-auction and the project sells out above base price, revenues must be withdrawn by the contract admin (not the artist alone). This protects collectors from an artist unilaterally inflating the sellout price.
!!!

---

### `Dutch Auction – exponential price decrease`

Price starts high and decays exponentially over time. Collectors pay the price at the time they purchase — earlier buyers pay more. No settlement mechanism.

**Best for:** Projects where price discovery is desired and collectors accept variable prices.

**Key parameters:**
- `startPrice`: Starting price in wei
- `basePrice`: Minimum resting price in wei
- `startTime`: Auction start timestamp
- `halfLifeSeconds`: Half-life of price decay

---

### `Dutch Auction – linear price decrease`

Price decreases linearly from start to end over a set duration. Predictable price curve.

**Best for:** Projects where a predictable, transparent price reduction curve is desired.

**Key parameters:**
- `startPrice`: Starting price in wei
- `basePrice`: Minimum resting price in wei
- `startTime`: Auction start timestamp
- `endTime`: Auction end timestamp

---

### `Dutch Auction – exponential, token holders only`

Extends the exponential Dutch Auction to require token holders of a specified collection to participate.

---

### `Dutch Auction – linear, token holders only`

Extends the linear Dutch Auction to require token holders of a specified collection to participate.

---

## Ranked Auction (RAM)

The Ranked Auction Minter (RAM) allows collectors to submit bids for a limited number of tokens. The highest bidders win; all winning bids pay the same price (the lowest winning bid).

Losing bidders receive automatic refunds. The ranked auction process runs non-custodially on-chain and scales to any project size. Artists may incur gas costs for minting tokens to winning bidders.

**Best for:** Projects with strong demand and a community-oriented ethos; "museum-quality" drops.

**Key parameters:**
- `auctionEndTime`: When bidding closes
- `numTokensToSell`: Number of tokens in the auction

---

## Serial English Auction (SEA)

The Serial English Auction (SEA) runs sequential English auctions for individual tokens. Inspired by [nouns.wtf](https://nouns.wtf/).

- Collectors kick off each token's auction by submitting a bid
- Any wallet can outbid; outbid amounts are refunded automatically
- Bids submitted near the end of an auction extend the auction window, ensuring human competitors can respond to bots
- Once an auction ends, the next token auction can be started alongside delivering the previous winner their token

The minter pre-mints tokens before their auction starts. Bids are placed on existing tokens, not hypothetical ones.

**Best for:** Long-running projects meant to be savored token-by-token; 1:1 auctions; community engagement over an extended period.

**Key parameters:**
- `auctionLengthSeconds`: Minimum duration per auction
- `minBidIncrementPercent`: Minimum increment for a new bid
- `startingPrice`: Minimum starting bid in wei

---

## Minimum Price Minter

Distributes tokens at near-zero cost. A small mint fee is sent to the render provider to help cover rendering and indexing costs.

**Best for:** Community giveaways, public art projects, accessibility-focused releases.

---

### `Minimum Price – allowlisted users only`

Extends the Minimum Price minter to restrict minting to an allowlist. Supports per-wallet limits.

---

## Polyptych Minter

The Polyptych (copy-hash) minter mints tokens with identical token hashes. This allows a project to produce multiple pieces that share a common generative seed — creating visual or conceptual cohesion across a set.

- Artists may mint child tokens to a parent token holder's wallet, or allow the parent holder to mint children themselves
- The artist's script must handle frame assignment by token number (e.g., tokens 0–99 render frame 1, tokens 100–199 render frame 2)
- Artists can increment the active frame on the minter

**Requires:** Configuration of the shared randomizer. Some interactions may need Etherscan/gnosis safe tx builder.

**Best for:** Multi-panel generative works, polyptych editions, companion pieces.

---

### `Polyptych – custom ERC20`

Extends the Polyptych minter to accept any ERC-20 token as payment.

---

## Custom Minters

Engine partners can add custom minters for their contracts. See [Custom Minters](/developer/minter-suite/custom-minters/) for the integration process.
