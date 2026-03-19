---
order: 3
description: End-to-end workflow examples showing how tools chain together
---

# Workflows

Individual tools are useful. Chaining them together is where it gets interesting.

---

## Mint Pipeline

The core workflow: discover, evaluate, check eligibility, build transaction.

### Discover

```
"What Art Blocks projects are minting right now?"
```

`discover_live_mints` returns active projects with pricing, supply, and minter type:

| Project | Artist | Price | Remaining |
|---|---|---|---|
| Logoria | Srđan Šarović, Una Popović | 0.018 ETH | 129/144 |
| pool party | BASEMENT x Ryley-O | 0.05 ETH | 759/777 |
| Signal Boards | Stina Jones | 0.015 ETH | 210/500 |

Each result includes `lowestListing` (secondary floor), so an agent can compare mint price vs. floor before recommending a purchase.

### Evaluate

```
"Tell me more about Signal Boards"
```

`get_project` returns trait distributions, artist info, license, and script type. If the secondary floor (0.011 ETH) is below mint price (0.015 ETH), an agent can flag that buying on secondary may be cheaper.

### Check Eligibility

```
"Can vitalik.eth mint this?"
```

`check_allowlist_eligibility` resolves ENS names and checks gating. This is the branching point: eligible wallets proceed to purchase, ineligible wallets get a clear explanation of why.

### Build Transaction

```
"Build the mint transaction for vitalik.eth"
```

`build_purchase_transaction` returns a ready-to-sign EVM transaction:

```json
{
  "to": "0x0635...b085",
  "data": "0xae77c237...",
  "value": "15000000000000000",
  "chainId": 1
}
```

No ABI encoding required. Pass directly to a wallet signer. A `warnings` array surfaces issues like price changes or low supply before signing.

### Full Pipeline

```
discover_live_mints → get_project → get_project_minter_config
  → check_allowlist_eligibility
    → eligible: build_purchase_transaction → sign + submit
    → not eligible: explain reason, surface alternatives
```

---

## Portfolio + Recommendations

```
"What Art Blocks pieces does vitalik.eth own?"
```

`get_wallet_tokens` returns all tokens with project details, traits, and transfer history. Cross-reference with `discover_live_mints` to surface connections:

- "You own Friendship Bracelets, and it still has 35 remaining."
- "You own work by Matto. Their latest project is live now."

Use `get_artist` to expand into full catalogs: "Fidenza is sold out (floor: 18.8 ETH) but available on secondary."

---

## Catalog Research

```
"Tell me about Chromie Squiggle"
```

`discover_projects` searches the full catalog by name, artist, or tags. For sold-out projects (`complete: true`), an agent knows to skip the mint flow and surface secondary market data instead.

Combine with `get_artist` to build full artist profiles across their entire Art Blocks catalog.
