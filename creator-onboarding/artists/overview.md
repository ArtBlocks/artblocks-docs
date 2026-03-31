---
order: 1000
description: Overview of the Art Blocks artist journey — from script to mainnet launch.
---

# Artist Overview

This section is for artists who have been accepted to Art Blocks Studio and are preparing to launch a project on-chain. It covers the full journey from building your generative script to opening minting to the public.

---

## Who This Is For

- Artists with an accepted Art Blocks Studio application
- Generative artists building JavaScript-based projects for on-chain deployment
- Artists returning to launch a follow-up project

If you haven't applied yet, start at [artblocks.io/apply](https://artblocks.io/apply) or read the [offerings page](/creator-onboarding/offerings/) for context on what Art Blocks offers.

---

## What You'll Need

Before starting, make sure you have:

- A working generative JavaScript script
- [MetaMask](https://metamask.io/) or another EVM-compatible wallet
- A small amount of Sepolia testnet ETH for test minting ([Sepolia faucets](https://www.alchemy.com/faucets/ethereum-sepolia))
- Access to the [Art Blocks Creator Dashboard](https://create.artblocks.io/) with your artist wallet

---

## The Journey at a Glance

```
Build → Stage → Review → Launch
```

1. **[Build your project](/creator-onboarding/artists/1-building-your-project/)** — Write a script that uses `tokenData.hash` as its randomness source. Define token traits with `window.$features`. Test for determinism and cross-browser compatibility.

2. **[Stage and test](/creator-onboarding/artists/2-staging-and-testing.md)** — Create a testnet project on Sepolia using the Creator Dashboard. Upload your script, configure details and payments, mint 20–40 test outputs, and submit for Art Blocks review.

3. **Review** — The Art Blocks team reviews your testnet project and provides feedback. Revisions may be requested before mainnet approval.

4. **[Launch on mainnet](/creator-onboarding/artists/3-mainnet-launch.md)** — Create your mainnet project shell, import configuration from testnet, mint token #0, and open minting to the public.

---

## Key Resources

- [Art Blocks Creator Dashboard](https://create.artblocks.io/) — project setup, script upload, minter configuration
- [Artist Staging](https://artist-staging.artblocks.io/) — testnet preview environment
- MCP Server: `scaffold_artblocks_project` — generate a ready-to-run starter script in under a minute
- Discord: `#artist-tech` and `#artist-general`
