# 2. Staging & Testing

Once your script is working locally, you'll create a testnet project using the Art Blocks Creator Dashboard and prepare it for review. This step covers the full staging process on Sepolia testnet.

---

## Before You Start

- Your script is complete and tested locally with many different hashes
- You have your artist wallet ready (the one registered with Art Blocks)
- You have some Sepolia ETH for test minting
- You have access to the [Creator Dashboard](https://create.artblocks.io/)

!!!warning
For your Art Blocks application, please connect with a hot wallet. Hardware wallets are not currently compatible with Art Blocks staging.
!!!

### Getting Sepolia ETH

Sepolia ETH is free and has no real value. You can request it from any of the following faucets:

- [sepoliafaucet.com](https://sepoliafaucet.com) — 0.5 per day, requires free Alchemy account
- [sepolia-faucet.pk910.de](https://sepolia-faucet.pk910.de) — min 0.01, max 2.5, PoW mining required, very energy and time consuming
- [coinbase.com/faucets/ethereum-sepolia-faucet](https://coinbase.com/faucets/ethereum-sepolia-faucet) — 0.5 per day, requires Coinbase wallet
- [faucet.quicknode.com/ethereum/sepolia](https://faucet.quicknode.com/ethereum/sepolia) — 1 drip per 12 hours, requires 0.001 ETH in wallet
- [infura.io/faucet/sepolia](https://infura.io/faucet/sepolia) — 0.5 per day, requires free Infura account
- [cloud.google.com/application/web3/faucet/ethereum/sepolia](https://cloud.google.com/application/web3/faucet/ethereum/sepolia) — 0.05 per day

---

## Creator Dashboard Overview

The [Art Blocks Creator Dashboard](https://create.artblocks.io/) is the primary interface for setting up and managing your project. Connect your artist wallet to get started.

The dashboard is organized into sub-pages for your project:

- **Details** — project metadata (name, description, license)
- **Scripts** — upload your script file and configure your dependency
- **Renders** — aspect ratio, render delay, Canvas Mode, MP4 settings
- **Payments** — primary and secondary revenue splits
- **Minters** — minting mechanism configuration
- **Outputs** — browse your minted test outputs

---

## Step 1: Create a Testnet Project

1. Connect your artist wallet to [create.artblocks.io](https://create.artblocks.io/)
2. Ensure you're on the **Sepolia** network
3. Click **Create New Project**
4. Your testnet project shell is now created

You'll see your new project listed in the dashboard. Click into it to begin configuration.

---

## Step 2: Details

Fill in your project metadata:

| Field | Notes |
|---|---|
| **Artist Name** | Your public artist name as it will appear on Art Blocks |
| **Project Name** | The title of the project |
| **Edition Size** | Total number of tokens (max invocations). Cannot be increased once locked. |
| **Description** | Artist statement / project description — visible on artblocks.io |
| **License** | NFT License, Creative Commons, or your custom license |
| **Website** | Artist website or project-specific URL (optional) |

!!!info
Submit one field at a time. Wait for that transaction to clear before attempting the next field.
!!!

### Writing Your Project Description

The project description is an important opportunity to highlight your intentions and provide an interpretative frame around how you want the viewer/collector to approach your project. Here are some prompts to help you get started:

- Begin with a strong, clear opening sentence.
- Lead with artistic inquiry; what questions can be prompted or answered through this work?
- How would you describe this project to someone unfamiliar with your work?
- What inspiration, color palette influences, themes, and techniques were used?
- Examine the outputs. What can the viewer see?
- Be sure to describe any interactivity features, if applicable.
- End by summarizing how the medium, outputs, and algorithm achieve your initial inquiry or concept.

---

## Step 3: Scripts

This is the core of your project setup.

1. **Script type & version** — Select your library (p5js, threejs, regl, etc.) and the version. This determines which library CDN the generator will load.
2. **Upload script** — Upload your `.js` file. The dashboard will show the script content for verification.
3. **PostParams** (Engine Flex only, optional) — If your project uses [Post-Mint Parameters](/protocol/postparams/), configure the parameters and standard hooks you want to use here. Artists may define on-chain configurable parameters (enums, booleans, colors, etc.) that collectors can adjust after minting.
4. **Decentralized Storage Assets** (Engine Flex only, optional) — If your project uses IPFS/Arweave external assets, configure them here. See [Decentralized Storage Assets](/creator-onboarding/engine-partners/flex-assets/) for details.

!!!info
Once your project is locked (after final review), the script cannot be modified. Test thoroughly before requesting a lock.
!!!

After uploading, use the **Preview** button to open a live view of a test output and verify your script renders correctly.

### Updating Your Script

If you make changes to your script, you may refresh individual tokens by navigating to the **Outputs** tab and using the **Refresh queue**. Note that batch refreshes are limited to once per day.

---

## Step 4: Renders

Configure how the Art Blocks rendering infrastructure captures your artwork:

| Setting | Notes |
|---|---|
| **Aspect Ratio** | Width:height ratio of your artwork (e.g. `1` for square, `1.5` for landscape). Used for canvas sizing and thumbnail display. |
| **Render Delay** | Seconds the renderer waits before capturing the static image. Set this long enough for any animations to complete their initial state (e.g. `0` for immediately deterministic art, `5` for animated pieces). |
| **Canvas Mode** | Enable if your script uses a `<canvas>` element directly (most p5.js and vanilla JS projects). Required for static capture to work correctly. |
| **MP4 Settings** | Optional. Configure if you want animated MP4 thumbnails generated for your project. |

---

## Step 5: Payments

Configure how primary and secondary revenues are split.

### Primary Sales

By default, primary sales split 90% to the artist and 10% to Art Blocks. You can add an additional payee to further split the artist's share (e.g. for collaborators or charitable giving).

- **Additional payee wallet** — Another Ethereum address to receive a portion of primary sales
- **Artist % to additional payee** — What percentage of the *artist's* primary share goes to the additional payee

### Secondary Royalties

Art Blocks contracts use ERC-2981 and [0xSplits](https://splits.org/) for secondary royalties. When you configure payment information, a splitter contract is automatically deployed.

- **Artist royalty %** — Typical range is 5%. This is the total secondary royalty paid to artist + any additional payee.
- **Artist secondary payee** — Additional address to split secondary royalties with the artist
- **Artist % to secondary payee** — Portion of artist's secondary share going to the additional payee

Your royalty splitter address is shown in the dashboard. You can view and withdraw balances at [app.splits.org](https://app.splits.org).

---

## Step 6: Minters

Choose your minting mechanism. For detailed guidance on each option, see the [Minter Guide](/creator-onboarding/artists/minters/).

Options include:

- **Set Price (ETH)** — Fixed price, first-come-first-served
- **Dutch Auction (w/ Settlement)** — Fair price discovery; all buyers pay the final price
- **Dutch Auction (exponential/linear)** — Price decreases over time; no settlement
- **Allowlist** — Fixed price for pre-approved wallets
- **Ranked Auction (RAM)** — Bid-based; all winning bidders pay the lowest winning bid

!!!info
A great option for testing is to select the **Minimum fee minter**. This will result in test mints costing 0.0015 ETH. If choosing **Set price - ETH**, set the minimum price of 0.015 ETH in order to save Sepolia ETH.
!!!

---

## Step 7: Test Minting

With your project configured, mint test outputs:

1. **Mint at least 20–40 test tokens** — enough to see meaningful variety across your trait space
2. **Use "Explore Possibilities"** in the Outputs tab — this previews many different hashes rapidly without spending gas on minting transactions
3. **Review outputs carefully** — look for visual errors, edge cases, extreme outputs
4. **Preview at** [artist-staging.artblocks.io](https://artist-staging.artblocks.io/) — this mirrors how your project will appear on artblocks.io

### What to Check

- [ ] Every output renders without errors
- [ ] Trait distribution is what you expect (check `window.$features` values)
- [ ] No hash produces a broken or undesirable output
- [ ] Artwork looks correct at different viewport sizes
- [ ] Render delay is long enough for animated pieces to settle

---

## Step 8: Submit for Review

When your testnet project is ready:

1. **Email [apply@artblocks.io](mailto:apply@artblocks.io)** with a link to your testnet project shell
   - Format: `https://artist-staging.artblocks.io/engine/[flex OR fullyonchain]/projects/[contractAddress]/[projectId]`
2. **Share your testnet project in `#artist-tech`** on Discord if you have technical questions
3. **Wait for feedback** — the Art Blocks team will review and may request changes before approving the mainnet deployment

Revisions may be requested before approval. Common feedback includes: output quality, trait distribution, edge-case handling, and script performance.

---

## Common Issues

| Issue | Fix |
|---|---|
| Script renders correctly locally but not in dashboard preview | Remove any CDN `<script>` tags from your script; check for DOM setup code that creates elements the generator already provides |
| Different outputs on reload with same hash | Remove `Math.random()` and `Date.now()` — seed all randomness from `tokenData.hash` |
| Static capture shows blank or mid-animation frame | Increase render delay in Renders settings |
