---
order: 600
description: Artist guide to Art Blocks minting mechanics — choosing and configuring a minter for your drop.
---

# Minters for Artists

The Art Blocks Minter Suite gives you control over how your project's tokens reach collectors. Choosing the right minting mechanism is one of the most important decisions in your project launch — it shapes who participates, at what price, and how fairly the drop unfolds.

This page covers minting from the artist's perspective. For the full technical reference, see the [Minter Suite developer docs](/developer/minter-suite/overview/).

---

## How to Choose a Minter

Consider your project's audience and demand level:

| Scenario | Recommended Minter |
|---|---|
| Standard project, moderate demand | Set Price (ETH) |
| Rewarding existing community | Allowlist |
| High anticipated demand, want fair price discovery | Ranked Auction (RAM) |
| High anticipated demand, want fair price discovery | Dutch Auction with Settlement |

**General advice:** For highly anticipated projects, avoid low fixed prices — bots benefit disproportionately. Dutch Auctions with Settlement provide the most equitable outcome for collectors when demand is high.

---

## Set Price (ETH)

The simplest option: all tokens sell at a fixed price in ETH, first-come-first-served.

**Configure in Creator Dashboard:**
- Set price per token in ETH
- Optionally set a minter-level max invocation cap (lower than project max)
- Unpause when ready to open

**When to use:** Moderate demand, clear target price, straightforward drop.

---

## Dutch Auction with Settlement (Exponential)

All collectors pay the same final price — the price at which the last token sold. Collectors who purchased above the final price receive an automatic settlement (refund of the difference).

This is Art Blocks' recommended minter for high-demand projects. It rewards patience and equalizes outcomes across all collectors.

**Configure in Creator Dashboard:**
- Start price (high)
- Resting/base price (minimum price the auction drops to)
- Start time
- Half-life (controls how fast the price drops — exponential curve)

**Half-life calculator:** The dashboard includes a half-life calculator tool. As a starting point:
- Short half-life (e.g. 5 min): Price drops quickly — good for shorter auctions
- Long half-life (e.g. 20 min): Gradual, extended price discovery

After all tokens are sold, the artist or admin collects revenues. Settlement claims are available to collectors immediately.

---

## Dutch Auction (Exponential or Linear, No Settlement)

Price starts high and drops over time. Collectors pay the price at the time they mint — no equalization after the fact.

- **Exponential**: Constant percentage decrease per unit time — feels "fair" and natural to collectors
- **Linear**: Constant absolute decrease per unit time — more predictable

**Configure:**
- Start price, base price, start time
- For exponential: half-life in seconds
- For linear: end time

---

## Allowlist

Fixed price restricted to pre-approved wallets. Artists provide a list of addresses; only those addresses can mint.

Optionally limit the number of mints per allowlisted address.

**How to create an allowlist:**
1. Collect wallet addresses of eligible collectors
2. In the Creator Dashboard, upload your list
3. The dashboard generates a Merkle root and configures the minter automatically

**When to use:** Rewarding early supporters, private sales, token-holder gating, community-exclusive drops.

---

## Ranked Auction (RAM)

Collectors submit bids during an auction window. The highest bidders win tokens; all winning bidders pay the lowest winning bid (equal final price). Losing bids are refunded.

Auctions run fully on-chain and non-custodially. Artists may incur gas costs to distribute tokens to winners after the auction closes.

**Configure:**
- Auction window (start and end time)
- Number of tokens available

**When to use:** High anticipated demand where fair price discovery matters — all winning bidders pay the same lowest winning bid.

---

## Minimum Price

Distributes tokens at near-zero cost. A small fee goes to the render provider. Good for public art or community giveaways.

Also available with an allowlist for controlled distribution at minimal cost.

---

## Mix and Match

You can use different minters for different phases. For example:

1. **Phase 1**: Allowlist at 0.1 ETH for 200 addresses, up to 1 mint each
2. **Phase 2**: Dutch Auction with Settlement starting at 0.5 ETH for the remaining tokens

Configure phases by setting per-minter max invocations and switching minters at the appropriate time.

---

## Tips

- **Test your minter configuration on testnet first.** The staging environment supports all minter types.
- **Coordinate timing with Art Blocks.** For public announcements and activation timing, work with your Art Blocks contact.
- **Communicate honestly.** If you pre-mint tokens for yourself or collaborators at below-public price, disclose this to your community.
- **Consider gas.** Launch during lower-gas periods to reduce friction for collectors.
- **For DA minters:** Check the half-life calculator to model price curves before finalizing. A starting price that's too high or a decay that's too slow can leave collectors uncertain.
