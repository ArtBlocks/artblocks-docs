---
order: 870
description: Creator Dashboard transaction, access, import, and output troubleshooting.
---

# Creator Dashboard Help

Start by checking the environment, chain, wallet, contract, and project ID shown in the dashboard. Most access and stale-data problems come from one of those values not matching the project you intended to edit.

For the end-to-end workflow, see the [Creator Dashboard guide](/creator-onboarding/artists/creator-dashboard/).

---

## Access and Project Visibility

**The project is missing.**

Confirm that you selected the right environment and chain before connecting. Reconnect with the registered artist wallet or a wallet granted access to the project contract.

**A field is read-only or an action is missing.**

Availability depends on your role, the contract version, the project state, and the selected chain. A locked project can also restrict editing.

The release checklist tracks a fixed set of release fields and whether each value is complete. It does not filter the list by your permissions. Check the field message and wallet status to see why an action is unavailable.

**The wallet is on a different network.**

Use the dashboard's network control, then approve the matching network in your wallet. Do not sign while the wallet and dashboard show different chains.

**I can see the project, but I cannot submit a transaction.**

Project visibility comes from your signed-in profile. On-chain changes use the active wallet, which must be an allowed signer for that field.

Follow the top-bar prompt to connect or switch wallets. If the correct wallet is connected and the field remains unavailable, your role, project lock state, or contract version may restrict it.

---

## Saves, Transactions, and Sync

**The dashboard says `Confirm in wallet…`.**

Open the wallet and inspect the request. Confirm it only if the network, account, contract, and action are correct. If no request appears, check for a hidden wallet window or reconnect the wallet.

**The transaction confirmed, but the dashboard says `Waiting for indexer…`.**

The chain transaction is complete, but the dashboard has not received the indexed data yet. Keep the page open and wait. Do not repeat the transaction solely because the old value is still visible.

**A save failed.**

Read the error before retrying. Confirm that the wallet has enough gas, the project is in the required state, and another transaction is not pending. Reload the project before retrying an action with an unclear result.

**The page looks stale.**

Wait for pending status messages to clear, then reload. Compare the value with a block explorer when the action was on-chain.

---

## Import Problems

**The source project is not listed.**

In the source window, connect with a wallet that owns the project or has contract access. Confirm that you opened the source environment selected by the dashboard.

**The import window did not open.**

Allow popups for the dashboard and select **Import project** again.

**The comparison does not include a field.**

Only supported fields can be imported. Configure any omitted or chain-specific value directly on the production project.

**An import stopped partway through.**

Use the retry action shown by the import when it is available. If you reload, check which destination values and transactions completed before importing only the remaining changes.

---

## Scripts and Outputs

**The script works locally but not in the dashboard.**

Remove CDN script tags that duplicate the selected dependency. Check for nondeterministic values such as `Math.random()` or `Date.now()`, and confirm that the script does not recreate DOM elements supplied by the generator.

**An output is blank or captures the wrong frame.**

Check **Render settings**. Increase the render delay, or use `window.$useRenderPreview` and `window.$renderPreview()` to identify the intended frame.

See [Thumbnail Capture](/creator-onboarding/artists/1-building-your-project/#thumbnail-capture-with-renderpreview) for the setup.

**Outputs still show an older script.**

Use the refresh action available for minted tokens in **View outputs**. Refresh is unavailable for **Samples** and completed projects.

Refreshes are queued and may take time. Avoid submitting the same refresh repeatedly.

---

## Other Dashboard Tools

- **Projects** lists projects you can access and their publication state.
- **Collectors** summarizes collector activity connected to your artist profile.
- **Insights** shows project and audience data available to your profile.
- **Contracts** lists the contracts your account can access.
- **Profile** is in the account menu and edits the artist profile linked to your sign-in.

If Collectors or Insights has no data, confirm that the correct artist profile is linked to your account. The **Artists** area is available only to Art Blocks staff.

---

## Before You Ask for Help

Include:

- Environment and chain
- Contract address and project ID
- Wallet address, if it is safe to share publicly
- Exact action and error text
- Transaction hash for an on-chain action
- Whether the problem also occurs after a reload

Do not share seed phrases, private keys, passwords, or wallet backup files.

For technical support, use `#artist-tech` in Discord or your Art Blocks artist contact. For application and review questions, email [apply@artblocks.io](mailto:apply@artblocks.io).
