---
order: 900
---

# Manual Admin Operations

Some rarely used admin operations are not available in the Art Blocks Creator Dashboard. These operations are available via direct interaction with the contract via a service such as Etherscan or Gnosis Safe's Transaction Builder.

A few manual admin operations are detailed below.

## Update provider secondary royalties payment addresses or basis points

> Note: this describes the process for updating provider secondary royalty information - artist updates are handled within the [Art Blocks Creator Dashboard](./dashboard.md).

For all V3 contracts, the contract admin can update the provider secondary royalties payment addresses or basis points by calling any of the following functions on the contract:

- `function updateProviderSalesAddresses`
- `function updateProviderPrimarySalesPercentages`
- `function updateProviderSecondarySalesBPS` or `function updateProviderDefaultSecondarySalesBPS` (depending on minor version)

For v3.2+ contracts (deployed after May 2024), the contract admin must also propagate the contract-level changes to every project in the contract by calling the following function on the contract for each project:

- `syncProviderSecondaryForProjectToDefaults(uint256 projectId)`

> Note: The additional step of syncing provider secondary royalties to defaults was added in v3.2 to enable conformance to the ERC-2981 royalty info standard while remaining scalable within ethereum's block gas limit.
