# Artist FAQ

---

## Application

**How do I apply to Art Blocks?**
Apply at [artblocks.io/apply](https://artblocks.io/apply). Applications are reviewed on a rolling basis. The acceptance rate is approximately 10%.

**What does Art Blocks look for?**
Innovation in how generative code expresses artistic ideas, technical proficiency, and conceptual depth. Art Blocks is interested in work that pushes the boundaries of what the medium can do — not just technically polished, but genuinely interesting.

**I applied and haven't heard back. What should I do?**
Art Blocks reviews applications as a team and may take several weeks. If it's been more than a month, feel free to follow up at [apply@artblocks.io](mailto:apply@artblocks.io).

**Can I submit multiple projects for consideration at once?**
Generally, start with your strongest project. Once accepted and your first project launches, you're welcome to discuss future projects.

---

## Technical Requirements

**What programming languages are supported?**
JavaScript. Generative scripts must be written in JS and run in a standard browser environment.

**Can I use TypeScript?**
You must upload compiled JavaScript. Develop in TypeScript if you prefer, but compile to plain JS before uploading.

**Can I use multiple libraries?**
No — one library (one dependency) per project. Scripts are limited to a single external library from the Art Blocks Dependency Registry.

**What if my preferred library version isn't in the registry?**
Contact Art Blocks in `#artist-tech`. The team can evaluate adding new versions to the registry.

**Can I use ES modules or import statements?**
Only for libraries that use module-based delivery (e.g. Three.js v0.161+). The generator handles import map setup for registered module-based libraries. For standard UMD/IIFE libraries, the library is injected as a global.

**My script uses `Math.random()` — is that a problem?**
Yes. `Math.random()` is non-deterministic. Seed a PRNG from `tokenData.hash` instead. See [Building Your Project](/creator-onboarding/artists/1-building-your-project/) for the recommended sfc32 implementation.

**How large can my script be?**
Scripts are stored on-chain in segments of ~24KB. There's no hard limit, but scripts larger than ~200KB may incur significant gas costs. Optimize and minify where possible.

**Can I update my script after it's live?**
Scripts can be updated until the project is **locked**. Locking is permanent — after the lock, the script cannot be changed. Locking is required before a project sells out.

---

## Creator Dashboard

**My project shell disappeared from the dashboard. What happened?**
Try disconnecting and reconnecting your wallet. Make sure you're connected with your registered artist wallet.

**How do I preview my script in the Creator Dashboard?**
On the Scripts sub-page, click **Preview** after uploading your script. A new window will open with a live render.

**Can I import my testnet configuration to mainnet?**
Yes. The Creator Dashboard includes an **Import from Testnet** feature. Import Details, Scripts, Renders, Payments, and Minters — but skip Admin settings.

**What's the difference between Canvas Mode being on or off?**
If checked, data is directly pulled from the `Canvas` element using `.toDataURL()` when producing static image renders. This additional rendering mode can be leveraged for projects with varying aspect ratios across different tokens.

Please note that scripts containing multiple `Canvas` elements may not render as intended.

**I set up my payment splits wrong. Can I change them?**
You can update payment configuration up until the project is locked. After locking, the royalty splitter is immutable — contact Art Blocks to request a splitter replacement.

---

## Staging and Testing

**How do I get Sepolia testnet ETH?**
Use the [Alchemy Sepolia faucet](https://www.alchemy.com/faucets/ethereum-sepolia) or ask in `#artist-tech` on Discord — community members often share faucet access.

**How many test mints should I do before submitting for review?**
Mint at least 20–40 test tokens and use "Explore Possibilities" to preview many more hashes without spending gas.

**My script renders correctly locally but not in the dashboard preview. Why?**
Common causes: CDN `<script>` tags in your script (the generator injects the library — don't add your own), DOM setup code (e.g. creating a `<canvas>` element that already exists), or references to external resources.

**My static thumbnail shows a blank or mid-render frame. How do I fix this?**
Increase the Render Delay in your Renders settings. For animated pieces, set it long enough for the initial state to stabilize.

**Can I test PostParams on staging?**
Yes. Navigate to your token on artist-staging.artblocks.io and use the PostParam editing interface while logged in with your artist wallet.

---

## Artist Pipeline

**How long does review take?**
Typically 1–3 weeks. The Art Blocks team reviews each project carefully and may request revisions.

**What kind of feedback might I receive?**
Output quality, trait distribution, edge-case handling, script performance, and artistic considerations. Address all feedback before requesting re-review.

**What happens between testnet approval and mainnet launch?**
Art Blocks coordinates a mainnet deployment slot. You'll be notified, create your mainnet project, import from testnet, mint token #0, and then Art Blocks activates the project on the platform.

**Can I change the edition size after launch?**
Edition size can only be **decreased** on V3 contracts, never increased. Once tokens are minted past a reduced size, the size is fixed.

---

## Pricing and Revenue

**What percentage do I keep from primary sales?**
90% of primary sales go to the artist; 10% to Art Blocks.

**What are typical secondary royalties?**
Up to 5% total on secondary sales. By default, roughly 2/3 goes to the artist and 1/3 to Art Blocks. Artists configure the exact percentage in the Creator Dashboard.

**When can I withdraw royalties?**
Secondary royalties accumulate in your 0xSplits splitter contract. Distribute at any time by visiting [app.splits.org](https://app.splits.org) and triggering a distribution.

**Can I accept an ERC-20 token as payment?**
Yes, with the Set Price – ERC20 minter. Contact Art Blocks to confirm the token is supported.

---

## Security

**Should I use a hardware wallet?**
Yes, strongly recommended for your artist wallet, especially after project launch.

**My wallet was compromised. What do I do?**
Contact Art Blocks immediately at [apply@artblocks.io](mailto:apply@artblocks.io) and in `#artist-tech` on Discord. Artist address updates require a proposal/approval process.

**Can someone copy my script?**
Your script is stored on-chain and is publicly readable. To protect your work, ensure your project is locked before launch, so no modifications are possible.

---

## Post-Release

**Can I release future projects?**
Yes. Many Studio artists release multiple projects. Use the same Creator Dashboard account and artist wallet.

**My project sold out. Can I add more tokens?**
On V3 contracts, you cannot increase the edition size. You can release a follow-up project instead.

**I see my art being used without permission. What can I do?**
Art Blocks' standard license gives collectors the right to display their specific token, not to reproduce the project at scale. For licensing concerns, consult with a legal advisor familiar with NFT IP.

**How do I add animated thumbnails to my project after launch?**
Contact Art Blocks in `#artist-tech` with your animation settings (render delay, aspect ratio, MP4 specs).
