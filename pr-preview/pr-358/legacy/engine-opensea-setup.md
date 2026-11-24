# Legacy: Engine OpenSea Setup

!!!warning
This page documents a legacy manual process for configuring OpenSea storefronts for Engine contracts. Current V3.2+ contracts handle royalties on-chain via ERC-2981 and do not require this manual setup. Contact Art Blocks if you have questions about your specific contract version.
!!!

---

## OpenSea Storefront Ownership Transfer

After the first token has been minted on your new Art Blocks Engine contract, you should be able to see this token in the OpenSea storefront at the format:

```
https://opensea.io/assets/{CONTRACT_ADDRESS}/{TOKEN_ID}
```

Once this first token is populated, the Art Blocks team will transfer the OpenSea collection for your project to a wallet you control. By default, Art Blocks will use the same address designated as the admin of your smart contract.

If you prefer a different wallet address for OpenSea collection management, contact Art Blocks **before** the collection is transferred.

After your designated wallet is added as the collection administrator, you may remove the Art Blocks-controlled wallet from admin access. The Art Blocks wallet is added automatically at collection creation time. **We recommend removing it so that only you control your OpenSea storefront.**

---

## OpenSea Storefront Options

For Art Blocks Engine projects, OpenSea supports two collection organization options:

**Option 1: All projects in one collection**

All projects on your Engine contract are grouped in a single large OpenSea collection. Individual projects appear as filter traits in the sidebar.

**Option 2: Each project as its own collection**

Each new project on your contract is handled as its own separate collection on OpenSea, with project traits as properties.

By default, collections are organized via Option 1. To request Option 2, contact the Art Blocks team and we can facilitate the change with OpenSea on your behalf.
