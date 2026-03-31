---
order: 600
description: Frequently asked questions for Art Blocks Engine partners.
---

# Engine Partner FAQ

---

## Getting Started

**How long does the full onboarding process take?**
From initial outreach to mainnet contract deployment, typically 6–12 weeks. The partner-side integration (connecting your frontend) varies widely and can extend the timeline depending on your team's bandwidth.

**What networks does Art Blocks Engine support?**
Ethereum mainnet, Arbitrum One, and Base. Contact your account manager for current availability on each network.

**Can I deploy on multiple networks?**
Yes, with separate contracts per network. Discuss your multi-chain requirements during scoping.

**Can I have multiple contracts?**
Yes. Some partners run separate contracts for different brands, platforms, or artist programs.

---

## Projects and Artists

**How do I add new projects to my contract?**
The contract admin calls `addProject` on your Engine core contract (via Etherscan, Gnosis Safe, or your admin dashboard). After creating the shell, the artist can configure details via the Art Blocks Creator Dashboard.

**When does a project lock?**
Project scripts lock permanently when the admin or artist triggers the lock. Once locked, the script cannot be changed. On V3 contracts, the project size (max invocations) cannot be increased after any tokens are minted.

**What is the difference between `paused` and `active`?**

| State | Visible Publicly | Purchasable |
|---|---|---|
| Inactive + paused (default) | No | No |
| Active + paused | Yes | Artist wallet only |
| Active + unpaused | Yes | Anyone |

Activation is done by the contract admin. Unpausing is done by the artist.

**How long does it take for a newly created project to appear on the Art Blocks indexer?**
The Art Blocks subgraph and API typically index new projects within a few minutes of contract activity. If your project isn't appearing after 10–15 minutes, contact Art Blocks support.

---

## Minting

**What minters are available to Engine partners?**
All globally approved minters from the shared Minter Suite: Set Price (ETH, ERC20, allowlist, token-holder gated), Dutch Auction (with/without settlement, exponential/linear), Ranked Auction (RAM), Serial English Auction (SEA), Minimum Price, and Polyptych. See the [Minters catalog](/developer/minter-suite/minters/).

**Can we use a custom minter?**
Yes. Engine partners can add custom, one-off minters to their contracts. See [Custom Minters](/developer/minter-suite/custom-minters/) for the process. Custom minters are not indexed by the Art Blocks subgraph and must be configured via your own frontend or Etherscan.

**What is the difference between project max invocations and minter max invocations?**
- **Project max invocations** is set on the core contract and is the hard cap — the project can never mint more tokens than this.
- **Minter max invocations** is set on the minter and can be lower than the project max. This allows you to cap a phase (e.g. allowlist can only mint 200 tokens even though the project size is 500).

**Can the project size be increased after launch?**
On V3 contracts, max invocations can only be decreased, never increased. Once tokens are minted past a reduced size, the size is fixed.

**Does the GPU rendering service handle Engine projects?**
Yes. The Art Blocks rendering infrastructure (media proxy, generator API) handles Engine projects the same as flagship projects.

---

## Technical

**What is the maximum number of external asset dependencies for Flex projects?**
There is no hard cap, but performance considerations apply. Fetching many external assets at render time increases load time. Test with your specific configuration.

**How do I update my contract's preferred IPFS or Arweave gateway?**
Contact the Art Blocks team. Gateway updates are applied at the contract level by Art Blocks.

**Can artists update their royalty configuration after launch?**
Yes, royalty configuration (artist splits, additional payees) can be updated up until the project is locked. On V3.2+ contracts using 0xSplits, changing splits requires deploying a new splitter contract. Contact Art Blocks if the artist royalty wallet needs to be updated post-launch.

**What is `autoApproveArtistSplitProposals` and how do I set it?**
This flag must be set at contract deployment and cannot be changed afterward. If `true`, artists can update their royalty wallet without admin approval. If `false`, the contract admin must approve any royalty wallet changes.

---

## Royalties and Payments

**How are secondary royalties structured for Engine?**
V3.2+ Engine contracts use ERC-2981 royalties via 0xSplits. The splitter contract distributes secondary royalties to the artist, any additional payee, the platform (Engine partner), and Art Blocks per configured percentages. Typical total secondary royalty is 5–10%.
