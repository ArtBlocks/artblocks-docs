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
- You have the mainnet [Creator Dashboard](https://create.artblocks.io/) access

---

## Step 1: Create Your Mainnet Project Shell

1. Connect your artist wallet to [create.artblocks.io](https://create.artblocks.io/)
2. Switch to **Ethereum Mainnet** (or Arbitrum/Base if specified by your agreement)
3. Click **Create New Project**

Your mainnet project shell is now created with a project ID.

---

## Step 2: Import from Testnet

Rather than re-entering all your configuration, the Creator Dashboard supports importing from your testnet project. In your mainnet project, use the **Import from Testnet** feature:

- **Details** — Import project name, description, license, website, edition size
- **Scripts** — Import your script file and dependency configuration
- **Renders** — Import aspect ratio, render delay, Canvas Mode settings
- **Payments** — Import payment splits (a new royalty splitter will be deployed on mainnet)
- **Minters** — Import minter configuration (auction parameters, etc.)

!!!warning
Do **not** import the **Admin** settings from testnet. Admin settings contain testnet-specific configuration that should not be applied to mainnet.
!!!

After importing each section, verify the values are correct before saving.

---

## Step 3: Verify and Preview

Before minting token #0:

- [ ] All Details fields are correct (project name, description, edition size)
- [ ] Script is uploaded and the correct version is selected
- [ ] Renders settings match your testnet configuration
- [ ] Payment splits are configured correctly — verify the splitter address in the dashboard
- [ ] Minter is configured (for fixed price) or will open automatically (for auction minters)
- [ ] Click **Preview** on the Scripts page to view a test render on mainnet

---

## Step 4: Mint Token #0

Token #0 is traditionally the artist's token — the first mint of a project.

1. In the Outputs tab, click **Mint Token #0**
2. Confirm the transaction in your wallet
3. Wait for the transaction to confirm

After minting, your token will appear on [artblocks.io](https://artblocks.io) once it's indexed (typically within a few minutes).

Art Blocks will then **activate** your project, making it visible to the public on artblocks.io. You'll be notified when activation is complete.

---

## Step 5: Open Minting

Once your project is activated, you control when minting opens to the public.

### Fixed Price Minters

For Set Price minters: the project opens when you **unpause** it in the Creator Dashboard. 

State transitions:
- `inactive + paused` — private shell, no purchases possible (default)
- `active + paused` — publicly visible, but only the artist wallet can mint
- `active + unpaused` — **open to the public**

Unpause in the Creator Dashboard when you're ready to go live. Gas recommendations: mint during off-peak hours (weekends, late evenings US time) to avoid high gas prices that can reduce collector participation.

### Auction Minters

Dutch Auction and RAM minters open automatically at the configured start time. No manual unpause required — set your start time and the auction opens itself.

---

## Step 6: Communicate Your Launch

Let collectors know when minting opens. See the [Community guide](/creator-onboarding/artists/community/) for Art Blocks' communication guidelines around project announcements.

**Key timing guidelines:**
- Do not publicly announce specific launch details (price, date, time) until Art Blocks gives the green light
- Coordinate with your Art Blocks account manager on announcement timing
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

Once your first project is complete, you're welcome to apply for future projects. Many Studio artists release multiple projects over time. The same Creator Dashboard account and artist wallet can be used for subsequent projects.

### Feedback and Support

- Technical issues: `#artist-tech` on Discord
- General questions: `#artist-general` on Discord
- Email: [apply@artblocks.io](mailto:apply@artblocks.io)
