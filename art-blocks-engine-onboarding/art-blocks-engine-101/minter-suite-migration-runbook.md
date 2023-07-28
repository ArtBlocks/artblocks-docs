---
order: -5
---

# Minter Suite Migration Runbook

This page provides a step-by-step guide on how to migrate a V3 Art Blocks Engine core contract from the legacy non-shared minter suite to the new shared minter suite. This migration is required for all V3 Engine contracts that want to use the new shared minter suite, which has the following benefits:

- All minter contracts are indexed by the Art Blocks subgraph, and can therefore be configured in the Artist Dashboard
- All minter Art Blocks Flagship minting contracts become available for use by Engine projects
- The new minting SDK can be used to simplify Engine partners frontend minting codebases
- Collectors can purchase from the same trusted contract they interact with on Flagship.

Migration is not available for V2 Engine contracts; for Engine partners that wish to upgrade to a V3 Engine contract, please contact the Art Blocks team.

Migration is not required for V3 Engine contracts that wish to continue using the legacy non-shared minter suite. However, we recommend migrating to the new shared minter suite for the benefits listed above.

## Migration Steps

### 1. Engine partner frontend updated to support new minter suite

The Engine partner's frontend must be updated to support the new shared minter suite. To help with this transition, the Art Blocks team has created a new minting SDK that can be used to support the new shared minter suite. Documentation for the SDK will be referenced here when it becomes available.

### 2. Schedule downtime for any live projects

The migration process requires all artists with live projects configure a new minter. All live projects should be paused during the migration process. Switching to the new minter filter is simple, but after migrating to the new minter filter, the artist of every live project must configure their minter in the new minter suite. This is also only a few transactions, but it is fully reliant on coordinating with artists to be ready to re-configure their minters after switching to the new minter filter.

### 3. Core contract admin sends migration transactions (testnet before mainnet)

The Engine partner's core contract admin should send 2 transactions to the core contract:

1. Engine Admin calls `updateRandomizerAddress` on the core contract, passing in the address of the shared randomizer. The shared randomizer address will be populated here once the Art Blocks team deploys the shared randomizer contract to mainnet (as well as testnets).

2. Engine Admin calls `updateMinterContract` on the core contract, passing in the address of the shared minter filter. The shared minter filter address will be populated here once the Art Blocks team deploys the shared minter filter contract to mainnet (as well as testnets).

You are now using the new shared minter suite!

### 4. Artists re-configure minters for ALL LIVE PROJECTS

**AFTER** step 3, artists must re-configure their minters for **all live projects**. This is a quick process, but requires coordination with artists to ensure they are ready to re-configure their minters after the switch.

Artists can re-configure their minters via the Artist Dashboard. The Artist Dashboard is updated to support the new shared minter suite for Art Blocks Engine contracts. The process for _most_ open projects will likely be to switch to a fixed price minter. The steps to complete switching to a fixed price minter are:

1. Artist navigates to the Artist Dashboard via the `edit` button on their project page on the Art Blocks website (while connected with their artist wallet)
2. (recommended, but not required) Artist pauses their project
3. Artist selects the "Minter" tab
4. Artist selects the "Fixed Price ETH" minter and sends transaction to assign the minter to their project
5. (optional) If max invocations should be limited by the minter, Artist sets max invocations to desired value (sends transaction)
6. Artist sets the price per per token in wei (sends transaction)
7. Artist unpauses their project (if paused in step 2) (sends transaction)

Your project is now using the new shared minter suite and live for minting!

### 5. Engine partner monitors migration progress

It is recommended that the Engine partner monitor the migration process to ensure that all artists have successfully re-configured their minters. Additionally, the Engine partner should use diligence to ensure that purchases and payment splits after the migration are working as expected.

### 6. Add any custom minters to the shared minter suite

The new shared minter suite provides all Art Blocks Flagship minters to Engine projects. However, if the Engine partner has any custom, one-off minters that they would like to use for their core contract, they can be added for their specific contract. Please contact the Art Blocks team for assistance. Note that at this time, custom, one-off minters will not be indexed in the Art Blocks Subgraph or API. This is likely not a change for custom minters being used prior to migration.

Custom minters will need very slight modifications to work with the shared minter suite. This is because the minter must specify which core contract it is minting on to the minter filter contract. The Art Blocks team can assist with providing guidance on how to update one-off minters during the migration process, if needed.

### 7. Explore new minter suite features

The new shared minter suite provides all Art Blocks Flagship minters to Engine projects. Feel free to explore integrating new minters into your product!

## Migration FAQ

### What happens if an artist does not re-configure their minter?

If an artist does not re-configure their minter, their project will not be able to mint tokens. The artist will need to re-configure their minter before their project can mint tokens.

### What happens if an artist re-configures their minter incorrectly?

If an artist re-configures their minter incorrectly, best case scenario is that their project will not be able to mint tokens, and troubleshooting can identify the issue. Worst case scenario is that their project will be able to mint tokens, but the price per token will be incorrect (e.g. incorrect price entered) or the maximum invocations will be too high (e.g. forgot to set minter-max-invocations to a lower value than set on the core contract, if desired). For these reasons, artists should use diligence when re-configuring their minters.

### What happens if I migrate to the new shared minter suite?

If you migrate to the new shared minter suite, you will be able to use any new minters developed for Art Blocks Flagship. Additionally, you will be able to use the Artist Dashboard to configure your minters, because your minter suite will be indexed. You will also be able to use the new minting SDK to simplify your minting process.

### What happens if I do not migrate to the new shared minter suite?

If you do not migrate to the new shared minter suite, nothing will change, but you will miss out on new developments. You will not be able to use any new minters developed for Art Blocks Flagship. Additionally, you will not be able to use the Artist Dashboard to configure your minters, because your minter suite will not be indexed. You will need to continue to use the legacy non-shared minter suite.

### What happens if I migrate to the new shared minter suite, but I do not want to use the Artist Dashboard to configure my minters?

If you migrate to the new shared minter suite, but you do not want to use the Artist Dashboard to configure your minters, you can continue to configure your minters via your frontend, etherscan, etc., but your process will be slightly updated to support the new shared minter suite. The Art Blocks team can assist with providing guidance on how to update your process during the migration process if needed.

### What happens if I migrate to the new shared minter suite, but I do not want to use the new minting SDK?

If you migrate to the new shared minter suite, but you do not want to use the new minting SDK, you can continue to use your existing minting process, but your process will be slightly updated to support the new shared minter suite.
