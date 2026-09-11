---
order: 600
description: Transfer hooks — per-project contracts that Art Blocks Engine cores call on every mint and transfer.
---

# Transfer Hooks

A transfer hook is a contract that an Art Blocks Engine core calls every time a token in a project changes hands. The core calls it after the ownership write, on both mints and transfers, and passes it the token, the previous owner, the new owner, and the operator that initiated the move.

Hooks are configured per project, not per contract, so two projects on the same core can behave differently. A project with no hook configured behaves exactly as projects always have.

Because the hook is called as part of the transfer, **a hook that reverts aborts the mint or transfer**. That makes hooks a genuine extension point — a project can record provenance, emit richer events, or impose conditions on when a token may move — and it also makes them something a collector should look at before assuming a token is freely transferable.

## Compatibility

Transfer hooks require core version **v3.3.0 or later** (`GenArt721CoreV3_Engine`) or **v3.3.1 or later** (`GenArt721CoreV3_Engine_Flex`).

Support cannot be added to a contract that already exists. Engine cores are deployed as minimal proxies, and a proxy's implementation address is fixed in its bytecode at deployment, so an existing core will never gain hook support. Projects that need transfer hooks must live on a contract deployed after the v3.3 rollout. If you need a new core contract, contact the Art Blocks team.

To check a specific project, read the `supports_transfer_hooks` field described in [Reading the configuration](#reading-the-configuration) — it is `false` on every pre-v3.3 core.

## Configuring a hook

Either the artist or the contract's Admin ACL can set a project's hook:

```solidity
core.configureProjectTransferHook(projectId, hookAddress);
```

Passing `address(0)` clears the hook and returns the project to standard transfer behavior.

A non-zero hook must advertise the `ITransferHook` interface via ERC-165, using interface ID `0x6344b0e2`. The core rejects any address that does not. That ID is the selector of `onTokenTransfer` alone — Solidity excludes inherited interface functions from the XOR, so it does **not** include `IERC165`'s `0x01ffc9a7`.

The [Creator Dashboard](https://create.artblocks.io/) exposes this for projects on a supporting contract, letting an artist paste a hook address rather than send the transaction by hand.

## Locking

A project's hook configuration can be frozen permanently:

```solidity
core.lockProjectTransferHook(projectId, expectedHook);
```

Only the artist can lock, and locking is one-way. `expectedHook` must match the project's currently configured hook. That argument is not ceremony: the hook can be changed by either the artist or the Admin ACL, so without it a configuration transaction landing first could permanently lock in a hook nobody intended.

Locking at `address(0)` is meaningful — it guarantees the project will never have a transfer hook, which is a commitment a collector can rely on.

There is also an automatic lock. Every Art Blocks project's metadata locks four weeks after completion. If that window elapses while a project has **no** hook configured, the hook configuration is locked at `address(0)` too, and `configureProjectTransferHook` will revert from then on. A project that *does* have a hook set stays configurable past that point until the artist locks it explicitly.

!!!warning Locking freezes the address, not the behavior
Locking a project to an upgradeable proxy leaves that proxy's owner able to change what runs on every transfer, permanently, with no way for the project to move away from it. Only lock at an address whose code you have read and that cannot change.
!!!

## Reading the configuration

On chain:

```solidity
(address hook, bool locked) = core.projectTransferHookConfig(projectId);
```

Off chain, `projects_metadata` in the [Art Blocks GraphQL API](/developer/graphql/) carries three fields:

| Field | Meaning |
|---|---|
| `transfer_hook` | The configured hook address, or `null` if none |
| `supports_transfer_hooks` | Whether this project's core supports hooks at all |
| `transfer_hook_configuration_locked` | Whether the configuration can still change |

Use `transfer_hook_configuration_locked` rather than the raw `transfer_hook_locked` column. The raw column reflects only an explicit `lockProjectTransferHook` call, and it is `null` rather than `false` while unlocked — it does not account for the time-based automatic lock, which has no event to index and has to be derived when read.

Two events are emitted, and are indexed by the Art Blocks subgraph:

```solidity
event ProjectTransferHookUpdated(uint256 indexed _projectId, address indexed _hook);
event ProjectTransferHookLocked(uint256 indexed _projectId, address indexed _hook);
```

The automatic lock emits nothing, because no transaction causes it.

## Writing a hook

A hook implements a single function:

```solidity
interface ITransferHook is IERC165 {
    function onTokenTransfer(
        address coreContract,
        uint256 tokenId,
        address from,
        address to,
        address operator
    ) external;
}
```

- `from` is `address(0)` on mint.
- `operator` is the ERC-721 operator on a transfer, and on a mint it is the address that initiated the mint — the collector, not the minter contract.
- Reverting aborts the mint or transfer.

The recommended starting point is [`AbstractTransferHook`](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/contracts/engine/V3/transfer-hooks/AbstractTransferHook.sol), which satisfies the ERC-165 requirement and enforces that the caller really is the `coreContract` it was handed. Inheriting it, you implement `_onTokenTransfer` instead.

!!!danger Authenticate the core
`AbstractTransferHook` guarantees `msg.sender == coreContract`. It cannot know *which* cores your hook is supposed to serve. Without your own check that `coreContract` is a core you expect, any deployed contract can call your hook from its own address with whatever `tokenId`, `from`, `to`, and `operator` values it likes.

If your hook is meant to serve one project, also confirm the calling core has your hook configured for the project that `tokenId` belongs to.
!!!

Two more constraints worth designing around:

- **No reentrancy into the core.** For the duration of the hook call the core blocks mints and transfers across *every* project on that core. A hook that tries to mint or transfer on the calling core will revert the transaction that triggered it.
- **Gas is charged to the transferrer.** Every mint and every secondary transfer pays for the hook's work. Storage writes on each transfer are the usual cost driver, and an expensive hook makes the token more expensive to move for its whole life.

## Reference implementations

Art Blocks deploys two first-party hooks. Both are already deployed and verified, so a project can configure either without writing or deploying anything.

### OwnerHistoryTransferHook

Art Blocks deploys [`OwnerHistoryTransferHook`](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/contracts/engine/V3/transfer-hooks/OwnerHistoryTransferHook.sol) at `0x00000000cb60788043f4F779bfC192F1c5bd09FA` on every supported network. It records each token's chain of owners on chain and exposes it through `ownerHistory`, `previousOwners`, `lastRecordedOwner`, and `ownerHistoryLength`.

It is inert until a project opts in: it verifies with the calling core that it is the hook configured for that project, and reverts otherwise. It never blocks a transfer. Because it is already deployed and verified, a project wanting on-chain provenance can configure it directly without writing or deploying anything.

### MintTimeAndTransferCountHooks

[`MintTimeAndTransferCountHooks`](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/contracts/web3call/combined-hooks/MintTimeAndTransferCountHooks.sol) is a combined hook — a transfer hook *and* a [PostParams](/protocol/postparams/) read-augment hook in one contract. It records each token's mint timestamp and its count of ownership-changing transfers, and injects three values into the token's params on every read:

| Key | Value |
|---|---|
| `mintTimestamp` | Unix seconds of the mint block, or `"0"` if the hook was not configured before the mint |
| `secondsSinceMint` | Computed at read time, so it changes every block |
| `transferCount` | Ownership-changing transfers after the mint, excluding the mint itself |

Configure it as the project's transfer hook to record, and as its read-augment hook to inject. A project can do one without the other.

It also answers the re-render gotcha below. If the project configures a `transferCount` param with `Address` authorization pointing at this hook, the hook writes that value to the PMP contract on each counted transfer, which is what triggers an off-chain re-render. That write is `try`/`catch`'d and emits `TransferCountPMPSyncFailed` on failure, so a misconfigured param costs a stale image rather than a frozen collection.

| Network | Address |
|---|---|
| Mainnet, Arbitrum, Base, Shape, Sepolia (artist staging) | `0x000000002099d6BB23Ebd24aDCbee931ad461a39` |
| Sepolia (dev) | `0x2B530627ed72e3F77EAC0d1c8b3904E6d8f67c25` |

The two differ because the hook is constructor-bound to a PMP contract, and Sepolia dev runs its own PMP instance.

## Gotchas

**A hook does not re-render the token.** Running a hook is not a signal to the rendering pipeline, so a token's stored image and features stay as they were. This matters most for the projects most likely to want a hook: if the artwork reacts to its owner — say through the `InjectTokenOwner` augment hook — the live generator reflects the new owner immediately, while the thumbnail on artblocks.io and in marketplaces still shows the previous owner's output.

Writing a [PostParam](/protocol/postparams/) is the signal that does trigger a re-render, along with a recompute of the token's features. So a hook that needs the image to follow the transfer should write one from inside `onTokenTransfer` — which is exactly what [`MintTimeAndTransferCountHooks`](#minttimeandtransfercounthooks) does, if you would rather configure a deployed hook than write one. That works because a PostParam can be authorized to a specific address rather than to the artist or the collector: configure the parameter with the `Address` authorization option, set its authorized address to the hook contract, and the hook can then call `configureTokenParams` on the PMP contract as the transfer happens.

Two things to keep in mind if you do this. The core blocks reentrant mints and transfers for the duration of the hook, but not calls to other contracts, so writing to the PMP contract is allowed. And it is a storage write on top of a storage write — every transfer of every token in the project pays for both, forever.

**A hook affects mints, not just secondary transfers.** A hook that reverts under some condition will also block minting under that condition. Test the mint path.

**Setting a hook does not backfill.** A hook only sees transfers that happen after it is configured. Any history from before is not available to it.

**Clearing a hook does not undo its effects.** State a hook has already written stays written, and remains readable from the hook contract.

**Marketplaces may not anticipate a reverting hook.** A transfer that a hook rejects fails like any other failed transfer, which some interfaces surface poorly. Hooks that can block transfers deserve clear communication to collectors.

## Additional resources

- [`ITransferHook`](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/contracts/interfaces/v0.8.x/ITransferHook.sol) — the interface
- [`AbstractTransferHook`](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/contracts/engine/V3/transfer-hooks/AbstractTransferHook.sol) — recommended base contract
- [`OwnerHistoryTransferHook`](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/contracts/engine/V3/transfer-hooks/OwnerHistoryTransferHook.sol) — deployed reference hook
- [`MintTimeAndTransferCountHooks`](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/contracts/web3call/combined-hooks/MintTimeAndTransferCountHooks.sol) — deployed combined transfer + PostParams hook
- [PostParams](/protocol/postparams/) — the other major per-project extension point

Have an idea for a hook, or questions about whether one fits your project? Reach out to the Art Blocks team.
