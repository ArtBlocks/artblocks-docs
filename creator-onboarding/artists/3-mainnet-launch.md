---
order: 700
description: Launching your Art Blocks project on Ethereum mainnet — import, publish, and open minting.
---

# 3. Mainnet Launch

Once your testnet project has been approved by the Art Blocks team, you're ready to create your mainnet project and go live. This page covers the steps from mainnet deployment through opening minting to the public.

---

## Prerequisites

- Your testnet project has been reviewed and approved by Art Blocks
- You have your artist wallet ready with some ETH for gas
- You have access to the [Creator Dashboard](https://create.artblocks.io/) on mainnet

---

## Step 1: Create Your Mainnet Project Shell

1. Connect your artist wallet to [create.artblocks.io](https://create.artblocks.io/)
2. Switch to **Ethereum Mainnet** (or Arbitrum/Base if specified by your agreement)
3. Click **Create New Project**

Your mainnet project shell is now created with a project ID.

---

## Step 2: Import from Testnet

Rather than re-entering all your configuration, the Creator Dashboard supports importing from your testnet project. In your mainnet project, use the **Import from Testnet** feature to bring over:

- **Details** — project name, description, license, website, edition size
- **Scripts** — your script file and dependency configuration
- **Renders** — aspect ratio, render delay, Canvas Mode settings
- **Payments** — payment splits (a new royalty splitter will be deployed on mainnet)
- **Minters** — minter configuration (auction parameters, etc.)

!!!warning
Do **not** import the **Admin** settings from testnet. Admin settings contain testnet-specific configuration that should not be applied to mainnet.
!!!

!!!info
The artist address used when creating your mainnet project shell must match the one used on your testnet shell — this is what enables the Import Fields function to work. If your testnet and mainnet shells use different wallets, grant your mainnet wallet management access via the **Admin** tab of your testnet shell before importing.
!!!



After importing each section, verify the values are correct before saving.

---

## Step 3: Request a Script Review

Before moving to mainnet, you can request a script review from the Art Blocks team. The review verifies that your project meets Art Blocks' standards for resolution agnosticism and cross-browser/device compatibility.

To request a review, reach out via your artist Discord DM or post in `#artist-tech`. Please allow **3–5 business days** for completion once requested.

---

## Step 4: Verify and Preview

Before minting token #0, do a final check:

- [ ] All Details fields are correct (project name, description, edition size)
- [ ] Script is uploaded and the correct version/dependency is selected
- [ ] Renders settings match your testnet configuration
- [ ] Payment splits are configured correctly — verify the splitter address in the dashboard
- [ ] Minter is configured correctly

Use the **"View project page"** button in the top navigation of your mainnet project shell to preview how your project page will appear on Art Blocks. Your project is not yet visible to the public at this stage — this is a private preview for you as the artist. Use it to confirm that your project details, artwork renders, and metadata all look correct before proceeding.

---

## Step 5: Mint Token #0

Token #0 is traditionally the artist's token — the first mint of a project.

!!!warning
Before minting, confirm your **max invocations** (edition size) is set correctly. Once you mint token #0, you can only ever **decrease** this number. This is set on-chain and is irreversible. If left at the default of 1,000,000, your project will display as an open edition on the Art Blocks website.
!!!

1. In the Outputs tab, click **Mint token**
2. Confirm the transaction in your wallet
3. Wait for the transaction to confirm

---

## Step 6: Publish Your Project

Once token #0 is minted, click **"Publish project"** in the publishing panel on the right side of the Creator Dashboard. You'll be prompted to enter a **Start Date**.

Publishing makes your project page visible on Art Blocks and immediately adds it to the [Art Blocks Calendar](https://www.artblocks.io/calendar). Only published projects are visible on the Art Blocks website.

---

## Step 7: Open Minting

Once your project is published, you control when minting opens to collectors via the **"Open Minting"** button in the Creator Dashboard. For more detail on each minter type, see the [Minter Guide](/creator-onboarding/artists/minters/).

### Auction Minters (Dutch Auction, RAM)
Auction minters open automatically at the configured start date and time. No manual action is required — set your start time and the auction opens itself.

### Fixed Price Minters
For Set Price minters, you'll need to manually click **"Open Minting"** at your scheduled release time.

- Send the transaction **at least 30 seconds before** your intended release time
- Use **high gas (~2x** the suggested high gas on [etherscan.io/gastracker](https://etherscan.io/gastracker)**)** to ensure the transaction confirms in time

---

## Step 8: Communicate Your Launch

Let collectors know when minting opens. See the [Community guide](/creator-onboarding/artists/community/) for Art Blocks' communication guidelines around project announcements.

**Key timing guidelines:**
- Do not publicly announce specific launch details (price, date, time) until Art Blocks gives the green light
- Coordinate with your Art Blocks contact on announcement timing
- Art Blocks will promote your project via official channels on launch day

---

## After Launch

### Royalty Withdrawals

Secondary royalties accumulate in your 0xSplits splitter contract. To withdraw:

1. Visit [app.splits.org](https://app.splits.org)
2. Connect your wallet
3. Find your splitter contract (address shown in the Creator Dashboard)
4. Click **Distribute** to trigger a distribution to all payees

You can distribute at any time — there's no requirement to wait for the project to sell out.

### Animated Thumbnails

After launch, you can add animated thumbnails (MP4) to your project. Contact Art Blocks in `#artist-tech` if you'd like to add or update your animation settings.

### Returning for Future Projects

Many Studio artists release multiple projects. The same Creator Dashboard account and artist wallet can be used for subsequent projects. For projects that require screening, submit via your testnet shell and notify the team through your Discord artist DM.

### Feedback and Support

- Technical issues: `#artist-tech` on Discord
- General questions: `#artist-general` on Discord
- Email: [apply@artblocks.io](mailto:apply@artblocks.io)
