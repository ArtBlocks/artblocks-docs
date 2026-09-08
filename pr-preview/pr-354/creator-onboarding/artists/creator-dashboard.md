# Creator Dashboard V2

Use Creator Dashboard V2 to take a project from a test environment to its production release. The dashboard keeps the workflow focused with a release checklist, searchable settings, and clear transaction status.

This guide covers the journey. For specific failures and status messages, see [Creator Dashboard V2 Help](/creator-onboarding/artists/creator-dashboard-help/).

---

## Before You Start

Have these ready:

- An Art Blocks sign-in with a linked wallet
- A script tested locally across many hashes and viewport sizes
- Test-network ETH for transactions and preview mints
- Production-network ETH before launch

Anyone with an Art Blocks sign-in can create a staging project on the shared testnet contract. Production project access still follows Art Blocks approval.

Use the [staging Creator Dashboard](https://staging.create.artblocks.io/) for test projects and the [production Creator Dashboard](https://create.artblocks.io/) for mainnet projects.

Select the network before connecting your wallet, then confirm the network shown in the dashboard before changing a project.

Signing in and being ready to transact are separate. Your profile may show a project even when the active wallet cannot sign for it.

Follow any **Connect wallet**, **Switch wallet**, or **Switch to network** prompt before saving an on-chain change.

Some wallet extensions, including Rabby, may not change accounts when you select **Switch wallet**. Select the allowed account inside the extension, then reconnect if the prompt remains.

!!!warning
The test and production dashboards use separate project data and contracts. Confirm the environment, chain, contract, and project ID before every transaction.
!!!

---

## Stage and Test

### 1. Create or Open the Test Project

On staging, select **Create project**. If your profile is not allowlisted for a test contract, the dashboard creates the project on a shared testnet contract and Art Blocks submits the creation transaction for you.

Name the project and choose a linked wallet as its artist address. Keep the dialog open until the project finishes syncing. You will still need test ETH for later on-chain settings and test mints.

If your profile can create projects on another test contract, select that contract instead. You can also open an existing project from **Projects**.

Start on **Overview** and open the **Release checklist**. It separates required fields from optional fields and links each item to the right setting.

### 2. Use the Release Checklist

Work through the required items. The main project tabs are:

- **Details** for the project name, description, license, and website
- **Scripts** for the script, dependency, Flex assets, and PostParams
- **Render settings** for aspect ratio, render delay, and display settings
- **Minter** for the sale mechanism and its configuration
- **Payment** for primary splits and secondary royalties
- **Advanced** for contract-specific settings

Press `⌘K` on macOS or `Ctrl+K` on Windows and Linux to search project settings. The command bar can jump to a field, the release checklist, the script manager, or outputs.

The dashboard marks each save as either a wallet transaction or a direct data update.

For wallet transactions, keep the page open through both **Confirm in wallet…** and **Waiting for indexer…**. A confirmed transaction can take additional time to appear in the dashboard.

!!!warning
Read every wallet request before signing. Edition size can only be decreased. Locking external assets is irreversible, and the first script deployment changes how later script updates work.
!!!

Use the focused references when you need them:

- [Building Your Project](/creator-onboarding/artists/1-building-your-project/) for determinism, features, and thumbnail capture
- [Minters for Artists](/creator-onboarding/artists/minters/) for sale-mechanism tradeoffs
- [Decentralized Storage Assets](/creator-onboarding/artists/flex-assets/) for IPFS and Arweave assets
- [PostParams](/protocol/postparams/) for configurable post-mint parameters

### 3. Review Outputs

Select **View outputs** from the project page. **Samples** previews unminted renders across more hashes, while **Tokens** shows minted outputs.

To create a minted output, configure a fixed-price minter and price, then select **Mint**. Output minting only supports the fixed-price minter.

If your release uses another minter, use fixed price for test mints. Pause the project before switching to the final minter, then check its settings again.

Use both views to inspect the range of the algorithm. Art Blocks generally recommends at least 20–40 test mints before review.

Check that:

- Every output renders without errors
- The same hash always produces the same output
- Feature values and their distribution match your intent
- The work behaves at different viewport sizes
- Static captures show the intended frame

If a script changes, refresh the relevant token render or project renders and wait for the refresh to finish before reviewing again.

### 4. Submit for Review

Send Art Blocks the test project link through your artist contact or the agreed review channel. Keep the test project available while you address feedback.

---

## Move to Production

### 1. Open the Production Project

After approval, connect to the production environment and correct chain. Open the production project shell supplied by Art Blocks.

Check the contract address, project ID, artist address, and chain before continuing.

### 2. Import the Test Project

On the production project, select **Import project**.

The dashboard opens the source environment in a separate window. Sign in there with a wallet that owns the source project or has contract access, then choose the source project.

You do not need to download an export file. The source window prepares the export and returns it to the production import review.

Back in production, review the comparison between the current project and the import. Select only the fields you want to copy.

!!!warning
Import changes the production project and may require several wallet transactions. Verify the destination shown in the review, keep the page open, and do not switch networks until the import finishes.
!!!

Import can copy project metadata, render settings, the project script, Flex assets, and PostParams. You can uncheck individual changes before starting.

Import does not create the destination project or copy its edition size, artist address, payment settings, minter, status, outputs, or contract history. Configure and verify those values directly in production.

A script can be imported only before the destination has script chunks. Flex assets have similar contract-version and locking restrictions. A field omitted from the comparison must be configured directly.

### 3. Finish the Production Checklist

Open **Release checklist** again and use it to find the remaining required items. Publication itself appears in the checklist, so the checklist is guidance rather than a separate launch gate.

Confirm these values directly in production:

- Script and dependency version
- Max invocations
- Render settings
- Primary and secondary payment addresses
- Fixed-price minter and price for token #0
- Project status

Mint and inspect token #0 only after the irreversible values are correct and Art Blocks has cleared the project for that step.

If your release uses another minter, pause the project after token #0, configure the final minter, then reopen the checklist and verify its price, limits, and timing.

Payment changes may create a proposal that an allowlisted account must approve. Confirm the final on-chain addresses and percentages before launch.

### 4. Publish and Open Minting

Use **Publish project** to make the project visible when Art Blocks approves publication. Publishing and opening minting are separate actions.

If the project is paused, use **Open minting** before collectors should be able to mint. This project-level action is separate from the minter schedule.

For a minter with a start time, you can use **Open minting** as soon as the minter setup is final. The minter still blocks purchases until its start time. Pause minting before changing minters.

Coordinate the launch details with Art Blocks before announcing them. See the [Community Guide](/creator-onboarding/artists/community/) for release communication.

---

## After Launch

- Watch the first public mints and confirm outputs and metadata resolve normally.
- Pause minting before changing settings when the dashboard instructs you to do so.
- Use the splitter address shown under **Payment** to manage secondary royalties at [0xSplits](https://app.splits.org).
- Contact Art Blocks before changing a live project when the effect is unclear.

The previous dashboard workflow is still available in [Legacy Staging & Testing](/creator-onboarding/artists/2-staging-and-testing/) and [Legacy Mainnet Launch](/creator-onboarding/artists/3-mainnet-launch/).
