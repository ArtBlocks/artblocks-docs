---
order: -5
---

# Minter Suite Migration Runbook

!!!warning
This documentation is a work in progress. Minter suite migration is ongoing, and initial migrations are being actively worked. Please reach out to the Art Blocks team with any questions.
!!!

This page provides a step-by-step guide on how to migrate a V3 Art Blocks Engine core contract from the legacy non-shared minter suite to the new shared minter suite. This migration is required for all V3 Engine contracts that want to use the new shared minter suite, which has the following benefits:

- All minter contracts are indexed by the Art Blocks subgraph, and can therefore be configured in the new Artist Dashboard website (coming soon)
- All minter Art Blocks Flagship minting contracts become available for use by Engine projects
- Collectors can purchase from the same trusted contract they interact with on Flagship.
- Art Blocks will release an SDK to simplify the minting process for Engine projects (coming soon)

Migration is not available for V2 Engine contracts; for Engine partners that wish to upgrade to a V3 Engine contract, please contact the Art Blocks team.

Migration is not required for V3 Engine contracts that wish to continue using the legacy non-shared minter suite. However, we recommend migrating to the new shared minter suite for the benefits listed above.

## Migration Steps

### 1. Engine partner frontend updated to support new minter suite

The Engine partner's frontend must be updated to support the new shared minter suite. In general, the new shared minter suite requires the following changes:

- When specifying a project to configure or purchase from, an additional input arg of `coreContract` (address) must be specified. This is because one minter/minter filter contract is used for many core contracts.
- View functions on the minter contracts may have changed slightly. This is due to some minor architectural changes to the minter contracts that we believe simplifies their codebase and make them more extensible.

The source code of all new, shared minter contracts is available on the [Art Blocks smart contracts monrorepo](https://github.com/ArtBlocks/artblocks-contracts/tree/main/packages/contracts/contracts/minter-suite/Minters). The complete list of all new, shared minter contracts is:

- MinterSetPriceV5
- MinterSetPriceERC20V5
- MinterSetPriceMerkleV5
- MinterSetPriceHolderV5
- MinterSetPricePolyptychV5
- MinterSetPricePolyptychERC20V5
- MinterDAExpV5
- MinterDALinV5
- MinterDAExpHolderV5
- MinterDALinHolderV5
- MinterDAExpSettlementV3

!!!info
In the coming months, the Art Blocks team will be releasing a new minting SDK that can be used to support the new shared minter suite. Documentation for the SDK will be referenced here when it becomes available.
!!!

### 2. Schedule downtime for any live projects

The migration process requires all artists with live projects configure a new minter. All live projects should be paused during the migration process. Switching to the new minter filter is simple, but after migrating to the new minter filter, the artist of every live project must configure their minter in the new minter suite. This is also only a few transactions, but it is fully reliant on coordinating with artists to be ready to re-configure minters of open projects after switching to the new minter filter.

### 3. Core contract admin sends migration transactions (testnet before mainnet)

The Engine partner's core contract admin should send 2 transactions to the core contract:

1. Engine Admin calls `updateRandomizerAddress` on the core contract, passing in the address of the shared randomizer. The shared randomizer address will be populated here once the Art Blocks team deploys the shared randomizer contract to mainnet (as well as testnets).

2. Engine Admin calls `updateMinterContract` on the core contract, passing in the address of the shared minter filter. The shared minter filter address will be populated here once the Art Blocks team deploys the shared minter filter contract to mainnet (as well as testnets).

You are now using the new shared minter suite!

### 4. Artists re-configure minters for ALL LIVE PROJECTS

**AFTER** step 3, artists must re-configure their minters for **all live projects**. This is a quick process, but requires coordination with artists to ensure they are ready to re-configure their minters after the switch.

Artists can re-configure their minters manually by following the instructions documented in the [engine project launch/assigning a minter section](./Engine-project-launch.md#assigning-a-minter-v3-only-new-shared-minter-suite). Additionally, soon, artists will be able to configure their project minters via the (new) Artist Dashboard.

The process for _most_ open projects will likely be to switch to a fixed price minter.

After configuring a minter, the project is now using the new shared minter suite and live for minting!

### 5. Engine partner monitors migration progress

It is recommended that the Engine partner monitor the migration process to ensure that all artists have successfully re-configured their minters. Additionally, the Engine partner should use diligence to ensure that purchases and payment splits after the migration are working as expected.

### 6. Add any custom minters to the shared minter suite

The new shared minter suite provides all Art Blocks Flagship minters to Engine projects. However, if the Engine partner has any custom, one-off minters that they would like to use for their core contract, they can be added for their specific contract. Please see the [section below](#adding-a-custom-one-off-minter-to-the-shared-minter-suite) for steps on how to do this. Note that at this time, custom, one-off minters will not be indexed in the Art Blocks Subgraph or API. This is likely not a change for custom minters being used prior to migration.

Custom minters will need very slight modifications to work with the shared minter suite. This is because the minter must specify which core contract it is minting on to the minter filter contract. The Art Blocks team can assist with providing guidance on how to update one-off minters during the migration process, if needed.

### 7. Explore new minter suite features

The new shared minter suite provides all Art Blocks Flagship minters to Engine projects. Feel free to explore integrating new minters into your product!

## Adding a custom, one-off minter to the shared minter suite

Some Engine partners may wish to implement custom, one-off minters to the shared minter suite. This is able to be done by the admin of an Engine partner's core contract. The steps to add a custom, one-off minter to the shared minter suite are as follows:

### 1. Write the custom minter contract

The Engine partner will need to write the custom minter contract. The Art Blocks team can assist with providing guidance on how to translate a previously written, non-shared custom minter contract to be compatible with the new shared minter suite, if needed.

### 2. Deploy the custom minter contract

The Engine partner will need to deploy the custom minter contract to the desired network.

### 3. Allowlist the minter for the core contract on the shared minter filter contract

The Engine partner will need to allowlist the custom minter contract for their contract, on the shared minter filter contract. This is done by doing the following:

- Engine Admin calls `approveMinterForContract` on the shared minter filter contract, passing in the address of their core contract, and the custom minter contract

The custom minter is now ready to be used by projects on the Engine partner's core contract!

### 4. Artist configures the custom minter for their project

The artist will need to configure the custom minter for their project. Custom, one-off minters are not indexed by the Art Blocks subgraph (due to the minter being arbitrary and open-ended), so the artist will need to configure the custom minter via the Engine partner's frontend, etherscan, etc. Note that the typical minter filter function for setting a minter for a project, `setMinterForProject` should be used by the artist or admin to assign the custom minter for the project.

## Migration FAQ

### What happens if an artist does not re-configure their minter?

If an artist does not re-configure their minter, their project will not be able to mint tokens. The artist will need to re-configure their minter before their project can mint tokens.

### What happens if an artist re-configures their minter incorrectly?

If an artist re-configures their minter incorrectly, best case scenario is that their project will not be able to mint tokens, and troubleshooting can identify the issue. Worst case scenario is that their project will be able to mint tokens, but the price per token will be incorrect (e.g. incorrect price entered) or the maximum invocations will be too high (e.g. forgot to set minter-max-invocations to a lower value than set on the core contract, if desired). For these reasons, artists should use diligence when re-configuring their minters.

### What happens if I migrate to the new shared minter suite?

If you migrate to the new shared minter suite, you will be able to use any new minters developed for Art Blocks Flagship. Additionally, you will be able to use the Artist Dashboard to configure your minters, because your minter suite will be indexed. You will also be able to use the new minting SDK to simplify your minting process.

### What happens if I do not migrate to the new shared minter suite?

If you do not migrate to the new shared minter suite, nothing will change, but you will miss out on new developments. You will not be able to use any new minters developed for Art Blocks Flagship. Additionally, you will not be able to use the Artist Dashboard to configure your minters, because your minter suite will not be indexed. You will need to continue to use the legacy non-shared minter suite.

### What happens if I migrate to the new shared minter suite, but I do not want to use the (coming soon) Artist Dashboard to configure my minters?

There are many reasons why a partner might want to do this!

If you migrate to the new shared minter suite, but you do not want to use the Artist Dashboard to configure your minters, you can continue to configure your minters via your frontend, etherscan, etc., but your process will be slightly updated to support the new shared minter suite. Comparing the new minter contracts and the legacy minter contracts will help you understand the changes.

### What happens if I migrate to the new shared minter suite, but I do not want to use the new (coming soon) minting SDK?

No problem!

If you migrate to the new shared minter suite, but you do not want to use the new minting SDK, you can continue to use your existing minting process, but your process will be slightly updated to support the new shared minter suite.
