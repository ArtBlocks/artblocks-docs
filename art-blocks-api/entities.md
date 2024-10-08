---
sidebar_position: 2
title: Subgraph Entities
---

# Entities

- [`Project`](#project)
- [`ProjectScript`](#projectscript)
- [`ProposedArtistAddressesAndSplit`](#proposedartistaddressesandsplit)
- [`CoreRegistry`](#coreregistry)
- [`Contract`](#contract)
- [`Whitelisting`](#whitelisting)
- [`Account`](#account)
- [`AccountProject`](#accountproject)
- [`Token`](#token)
- [`MinterFilter`](#minterfilter)
- [`MinterFilterContractAllowlist`](#minterfiltercontractallowlist)
- [`Minter`](#minter)
- [`ProjectMinterConfiguration`](#projectminterconfiguration)
- [`Receipt`](#receipt)
- [`Transfer`](#transfer)
- [`ProjectExternalAssetDependency`](#projectexternalassetdependency)
- [`Dependency`](#dependency)
- [`DependencyRegistry`](#dependencyregistry)
- [`DependencyAdditionalCDN`](#dependencyadditionalcdn)
- [`DependencyAdditionalRepository`](#dependencyadditionalrepository)
- [`DependencyScript`](#dependencyscript)

# Project

Description: get various details about a specific project

| Field                                   | Type                                                               | Description                                                                                                                                        |
| --------------------------------------- | ------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| id                                      | ID!                                                                | Unique identifier made up of contract address and project id                                                                                       |
| projectId                               | BigInt!                                                            | ID of the project on the contract                                                                                                                  |
| active                                  | Boolean!                                                           | Determines if the project should be visible to the public                                                                                          |
| additionalPayee                         | Bytes                                                              | Address to split primary sales with the artist                                                                                                     |
| additionalPayeePercentage               | BigInt                                                             | Percentage of artist's share of primary sales that goes to additional payee                                                                        |
| additionalPayeeSecondarySalesAddress    | Bytes                                                              | Address to split Secondary sales with the artist                                                                                                   |
| additionalPayeeSecondarySalesPercentage | BigInt                                                             | Percentage of artist's share of secondary sales that goes to additional payee                                                                      |
| artist                                  | Account!                                                           | Artist that created the project                                                                                                                    |
| artistAddress                           | Bytes!                                                             | Wallet address of the artist                                                                                                                       |
| artistName                              | String                                                             | Artist name                                                                                                                                        |
| baseIpfsUri                             | String                                                             | Uniform Resource Identifier Interplanetary File System (IPFS) of a nonfungible token                                                               |
| baseUri                                 | String                                                             | The base URI is the mutual part among each NFT's URI. By default, the URI is baseURI/tokenId                                                       |
| complete                                | Boolean!                                                           | A project is complete when it has reached its maximum invocations                                                                                  |
| completedAt                             | BigInt                                                             | Timestamp at which a project was completed                                                                                                         |
| curationStatus                          | String                                                             | Curated, playground, factory. A project with no curation status is considered factory                                                              |
| currencyAddress                         | Bytes                                                              | ERC-20 contract address if the project is purchasable via ERC-20                                                                                   |
| currencySymbol                          | String                                                             | Currency symbol for ERC-20                                                                                                                         |
| description                             | String                                                             | Artist description of the project                                                                                                                  |
| dynamic                                 | Boolean!                                                           | Is the project dynamic or a static image                                                                                                           |
| invocations                             | BigInt!                                                            | Number of times the project has been invoked - number of tokens of the project                                                                     |
| ipfsHash                                | String                                                             | Interplanetary File System function that meets the encrypted demands needed to solve for a blockchain computation                                  |
| license                                 | String                                                             | License for the project                                                                                                                            |
| locked                                  | Boolean                                                            | For V3 and-on, this field is null, and projects lock 4 weeks after `completedAt`. Once the project is locked its script may never be updated again |
| maxInvocations                          | BigInt!                                                            | Maximum number of invocations allowed for the project                                                                                              |
| name                                    | String                                                             | Project name                                                                                                                                       |
| paused                                  | Boolean!                                                           | Purchases paused                                                                                                                                   |
| pricePerTokenInWei                      | BigInt!                                                            | Wei is the smallest denomination of ether—the cryptocurrency coin used on the Ethereum network. One ether = 1,000,000,000,000,000,000 wei (1018)   |
| royaltyPercentage                       | BigInt                                                             | Artist/additional payee royalty percentage                                                                                                         |
| script                                  | String                                                             | The full script composed of scripts                                                                                                                |
| scripts                                 | [`Project!`](#project)                                             | Parts of the project script                                                                                                                        |
| scriptCount                             | BigInt!                                                            | The number of scripts stored on-chain                                                                                                              |
| externalAssetDependencyCount            | BigInt!                                                            | The number of external asset dependencies stored on-chain                                                                                          |
| externalAssetDependenciesLocked         | Boolean!                                                           | Once the project's external asset dependencies are locked they may never be modified again                                                         |
| scriptJSON                              | String                                                             | Extra information about the script and rendering options                                                                                           |
| scriptTypeAndVersion                    | String                                                             | Script type and version (see `scriptJSON` if null)                                                                                                 |
| aspectRatio                             | String                                                             | Aspect ratio of the project (see `scriptJSON` if null)                                                                                             |
| tokens                                  | [`Token!`](#token)                                                 | Tokens of the project                                                                                                                              |
| useHashString                           | Boolean!                                                           | Does the project actually use the hash string                                                                                                      |
| useIpfs                                 | Boolean                                                            | Does the project use media from ipfs                                                                                                               |
| website                                 | String                                                             | Artist or project website                                                                                                                          |
| proposedArtistAddressesAndSplits        | ProposedArtistAddressesAndSplit                                    | Proposed Artist addresses and payment split percentages                                                                                            |
| owners                                  | [AccountProject!](#accountproject)                                 | Accounts that own tokens of the project                                                                                                            |
| createdAt                               | BigInt!                                                            | When project initiated                                                                                                                            |
| updatedAt                               | BigInt!                                                            | When project updated                                                                                                                               |
| activatedAt                             | BigInt                                                             | WHen project activated                                                                                                                             |
| scriptUpdatedAt                         | BigInt                                                             | when the script was updated                                                                                                                        |
| contract                                | Contract!                                                          | Contract associated to project                                                                                                                     |
| minterConfiguration                     | ProjectMinterConfiguration                                         | Minter configuration for this project (not implemented prior to minter filters)                                                                    |
| saleLookupTables                        | [SaleLookupTable!](#salelookuptable)                               | Lookup table to get the Sale history of the project                                                                                                |
| externalAssetDependencies               | [ProjectExternalAssetDependency!](#projectexternalassetdependency) | Projects external asset dependencies                                                                                                               |

# ProjectScript

Description: get specific details of the project script

| Field   | Type     | Description                                                  |
| ------- | -------- | ------------------------------------------------------------ |
| id      | ID!      | Unique identifier made up of contract address and project id |
| index   | BigInt!  | The dependency index                                         |
| project | Project! | Name of project                                              |
| script  | String!  | Script of the project                                        |

# ProposedArtistAddressesAndSplit

Description: get specific details on the pay flow for a specified artist

| Field                                   | Type     | Description                                                       |
| --------------------------------------- | -------- | ----------------------------------------------------------------- |
| id                                      | ID!      | Unique identifier made up of contract address and project id      |
| artistAddress                           | Bytes!   | Proposed artist address                                           |
| additionalPayeePrimarySalesAddress      | Bytes!   | Proposed artist additional payee address for primary sales        |
| additionalPayeePrimarySalesPercentage   | BigInt!  | Proposed artist additional payee percentage for primary sales     |
| additionalPayeeSecondarySalesAddress    | Bytes!   | Proposed artist additional payee address for secondary sales      |
| additionalPayeeSecondarySalesPercentage | BigInt!  | Proposed artist additional payee percentage for secondary sales   |
| project                                 | Project! | Project associated with this proposed artist addresses and splits |
| createdAt                               | BigInt!  | When address initiated                                            |

# CoreRegistry

Description: Get specific details on the Art Blocks Core registry. At this time, this is used for indexing purposes of V3 contracts, as well as acting as an allowlist of core contracts that may mint on a shared minter filter.

| Field               | Type        | Description                                                                                                                                                                                               |
| ------------------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id                  | ID!         | Unique identifier made up of the Core Registry's contract address. note: for legacy MinterFilters, this is a dummy ID, equal to the address of the single core contract associated with the minter filter |
| registeredContracts | [Contract!] | All core contracts that are registered on this CoreRegistry, when this is the most recent Core Registry to add the contract                                                                                   |

# Contract

Description: get specific information about contracts

| Field                                       | Type                           | Description                                                                                                                     |
| ------------------------------------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- |
| id                                          | ID!                            | Unique identifier made up of contract address                                                                                   |
| type                                        | CoreType!                      | Core contract type                                                                                                              |
| renderProviderAddress                       | Bytes!                         | Address that receives primary sales platform fees                                                                               |
| renderProviderPercentage                    | BigInt!                        | Percentage of primary sales allocated to the platform                                                                           |
| renderProviderSecondarySalesAddress         | Bytes                          | Address that receives secondary sales platform royalties (null for pre-V3 contracts, check Royalty Registry)                    |
| renderProviderSecondarySalesBPS             | BigInt                         | Basis points of secondary sales allocated to the platform (null for pre-V3 contracts, check Royalty Registry)                   |
| enginePlatformProviderAddress               | Bytes                          | Address that receives primary sales platform fees, only for V3_Engine contracts                                                 |
| enginePlatformProviderPercentage            | BigInt                         | Percentage of primary sales allocated to the platform, only for V3_Engine contracts                                             |
| enginePlatformProviderSecondarySalesAddress | Bytes                          | Address that receives secondary sales platform royalties, only for V3_Engine contracts                                          |
| enginePlatformProviderSecondarySalesBPS     | BigInt                         | Basis points of secondary sales allocated to the platform, only for V3_Engine contracts                                         |
| mintWhitelisted                             | [Bytes!]!                      | List of contracts that are allowed to mint                                                                                      |
| randomizerContract                          | Bytes                          | Randomizer contract used to generate token hashes                                                                               |
| curationRegistry                            | Bytes                          | Curation registry contract address                                                                                              |
| dependencyRegistry                          | Bytes                          | Dependency registry contract address                                                                                            |
| nextProjectId                               | BigInt!                        | Project ID listed on the contract                                                                                               |
| projects                                    | [Project!](#project)           | List of projects on the contract                                                                                                |
| tokens                                      | [Token!](#token)               | List of tokens on the contract                                                                                                  |
| whitelisted                                 | [Whitelisting!](#whitelisting) | Accounts whitelisted on the contract                                                                                            |
| createdAt                                   | BigInt!                        | When contract initiated                                                                                                         |
| updatedAt                                   | BigInt!                        | When contract updated                                                                                                           |
| minterFilter                                | MinterFilter                   | Associated minter filter (if applicable)                                                                                        |
| preferredIPFSGateway                        | String                         | The Engine Flex contract allows you to specify preferred gateways for the currently supported dependency types (IPFS & Arweave) |
| preferredArweaveGateway                     | String                         | The Engine Flex contract allows you to specify preferred gateways for the currently supported dependency types (IPFS & Arweave) |
| newProjectsForbidden                        | Boolean!                       | New projects forbidden (can only be true on V3+ contracts)                                                                      |
| autoApproveArtistSplitProposals             | Boolean                        | Automatically approve all artist split proposals (used on V3 Engine contracts)                                                  |
| registeredOn                                | EngineRegistry                 | Latest engine registry that this contract is registered with, if any (used for indexing purposes)                               |

# Whitelisting

Description: get whitelist information

| Field    | Type      | Description                            |
| -------- | --------- | -------------------------------------- |
| id       | ID!       | Unique identifier whitelist account id |
| account  | Account!  | Account associated to whitelisting     |
| contract | Contract! | contract associated to whitelisting    |

# Account

Description: get specific information about an account

| Field           | Type                               | Description                                  |
| --------------- | ---------------------------------- | -------------------------------------------- |
| id              | ID!                                | Unique identifier account id                 |
| tokens          | [Token!](#token)                   | Tokens the account has                       |
| projectsOwned   | [AccountProject!](#accountproject) | Projects the account owns tokens from        |
| projectsCreated | [Project!](#project)               | Projects the account is listed as artist for |
| whitelistedOn   | [Whitelisting!](#whitelisting)     | Contracts the account is whitelisted on      |

# AccountProject

Description: get project account information

| Field   | Type     | Description                   |
| ------- | -------- | ----------------------------- |
| id      | ID!      | Unique identifier token id    |
| account | Account! | Account associated to project |
| project | Project! | Name of project               |
| count   | Int!     | Total count of the project    |

# Token

Description: get various token information

| Field            | Type                                 | Description                                                                                  |
| ---------------- | ------------------------------------ | -------------------------------------------------------------------------------------------- |
| id               | ID!                                  | Unique identifier made up of contract address and token id                                   |
| tokenId          | BigInt!                              | ID of the token on the contract                                                              |
| contract         | Contract!                            | Contract the token is on                                                                     |
| invocation       | BigInt!                              | Invocation number of the project                                                             |
| hash             | Bytes!                               | Unique string used as input to the tokens project script                                     |
| owner            | Account!                             | Current owner of the token                                                                   |
| project          | Project!                             | Project of the token                                                                         |
| uri              | String                               | Specifies the endpoint for retrieving access tokens when OAuth 2.0 authentication is enabled |
| createdAt        | BigInt!                              | When token initiated                                                                         |
| updatedAt        | BigInt!                              | When token updated                                                                           |
| transactionHash  | Bytes!                               | Transaction hash of token mint                                                               |
| transfers        | [Transfer!](#transfer)               | Transfers of the token                                                                       |
| saleLookupTables | [SaleLookupTable!](#salelookuptable) | Lookup table to get the Sale history                                                         |
| nextSaleId       | BigInt!                              | Next available sale id                                                                       |

# MinterFilter

Description: get details about minters on a project

| Field                          | Type                              | Description                                                                                                      |
| ------------------------------ | --------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| id                             | ID!                               | Unique identifier made up of minter contract address                                                             |
| minterGlobalAllowlist          | [Minter!]!                        | Minters allowlisted globally on this MinterFilter                                                                |
| minterFilterContractAllowlists | [MinterFilterContractAllowlist!]! | Minters allowlisted at a contract-level on this MinterFilter                                                     |
| knownMinters                   | [Minter!](#minter)                | Known minters that are tied to this MinterFilter, but are not necessarily approved on this MinterFilter          |
| coreRegistry                   | [CoreRegistry!](#coreregistry)    | Core contract registry used by this MinterFilter. Note: For MinterFilter V0 and V1, a dummy CoreRegistry is used |
| updatedAt                      | BigInt!                           | When minter updated                                                                                              |

# MinterFilterContractAllowlist

Description: Defines a contract-specific allowlist of minters specifically approved on a given shared minter filter. This is used to extend the set of allowlisted minters beyond a shared minter filter's set of globally allowlisted minters.

| Field                   | Type          | Description                                                                                       |
| ----------------------- | ------------- | ------------------------------------------------------------------------------------------------- |
| id                      | ID!           | Unique identifier made up of {minter filter contract address}-{core contract address}             |
| minterFilter            | MinterFilter! | MinterFilter contract                                                                             |
| contract                | Contract!     | Core contract                                                                                     |
| minterContractAllowlist | [Minter!]!    | Minter contract addresses allowed at the contract level (extending global MinterFilter allowlist) |
| updatedAt               | BigInt!       | When last updated                                                                                 |

# Minter

Description: get details about mint on a project

| Field                               | Type          | Description                                                                            |
| ----------------------------------- | ------------- | -------------------------------------------------------------------------------------- |
| id                                  | ID!           | Unique identifier made up of minter contract address                                   |
| type                                | MinterType!   | Minter type                                                                            |
| minterFilter                        | MinterFilter! | Associated Minter Filter                                                               |
| isGloballyAllowlistedOnMinterFilter | Boolean!      | Boolean representing if the Minter is globally allowed on its associated minter filter |
| extraMinterDetails                  | String!       | Configuration details used by specific minters (json string)                           |
| receipts                            | [Receipt!]    | Receipts for this minter, only for minters with settlement                             |
| updatedAt                           | BigInt!       | When the minter updated                                                                |

# ProjectMinterConfiguration

Description: get details of a specific mint

| Field              | Type     | Description                                                                                     |
| ------------------ | -------- | ----------------------------------------------------------------------------------------------- |
| id                 | ID!      | Unique identifier made up of {minter contract address}-{core contract address}-{project number} |
| project            | Project! | The associated project                                                                          |
| minter             | Minter!  | The associated minter                                                                           |
| priceIsConfigured  | Boolean! | true if project's token price has been configured on minter                                     |
| currencySymbol     | String!  | currency symbol as defined on minter - ETH reserved for ether                                   |
| currencyAddress    | Bytes!   | currency address as defined on minter - address(0) reserved for ether                           |
| purchaseToDisabled | Boolean! | Defines if purchasing token to another is allowed                                               |
| basePrice          | BigInt   | price of token or resting price of Duch auction, in wei                                         |
| extraMinterDetails | String!  | Configuration details used by specific minter project configurations (json string)              |
| maxInvocations     | BigInt   | Maximum number of invocations allowed for the project (on the minter)                           |

# Receipt

Description: get details about purchases on a minter with settlement

| Field        | Type     | Description                                                                                                       |
| ------------ | -------- | ----------------------------------------------------------------------------------------------------------------- |
| id           | ID!      | Unique identifier made up of {minter contract address}-{core contract address}-{project number}-{account address} |
| project      | Project! | The associated project                                                                                            |
| minter       | Minter!  | The associated minter                                                                                             |
| account      | Account! | The associated account                                                                                            |
| netPosted    | BigInt!  | The total net amount posted (set to settlement contract) for tokens                                               |
| numPurchased | BigInt!  | The total quantity of tokens purchased on the project                                                             |
| updatedAt    | BigInt!  | Last updated timestamp                                                                                            |

# Transfer

Description: transfer info on an NFT

| Field           | Type    | Description                   |
| --------------- | ------- | ----------------------------- |
| id              | ID!     | Unique identifier of transfer |
| transactionHash | Bytes!  | transaction hash of transfer  |
| token           | Token!  | token address of NFT          |
| createdAt       | BigInt! | when transfer initiated       |
| to              | Bytes!  | address transferred to        |
| from            | Bytes!  | address transferred from      |

# ProjectExternalAssetDependency

Description: get info about projects external asset dependency

| Field          | Type                                | Description                                  |
| -------------- | ----------------------------------- | -------------------------------------------- |
| id             | ID!                                 | Unique identifier made up of projectId-index |
| project        | Project!                            | The associated project                       |
| dependencyType | ProjectExternalAssetDependencyType! | The dependency type                          |
| cid            | String!                             | The dependency cid                           |
| index          | BigInt!                             | The dependency index                         |

# Dependency

Description: information about registered dependency (e.g. p5js@1.0.0)

| Field                     | Type                                                                    | Description                                                                                         |
| ------------------------- | ----------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| id                        | ID!                                                                     | Unique identifier made up of dependency name and version separated by an @ symbol (e.g. p5js@1.0.0) |
| preferredCDN              | String!                                                                 | Preferred CDN for this dependency                                                                   |
| additionalCDNs            | [\[DependencyAdditionalCDN!\]!](#dependencyadditionalcdn)               | Additional CDNs for this dependency                                                                 |
| additionalCDNCount        | BigInt!                                                                 | Number of additional CDNs for this dependency                                                       |
| preferredRepository       | String!                                                                 | Preferred repository for this dependency                                                            |
| additionalRepositoryCount | BigInt!                                                                 | Additional repositories for this dependency                                                         |
| additionalRepositories    | [\[DependencyAdditionalRepository!\]!](#dependencyadditionalrepository) | Number of additional repositories for this dependency                                               |
| scripts                   | [\[DependencyScript!\]!](#dependencyscript)                             | List of on-chain scripts that for this dependency                                                   |
| scriptCount               | BigInt!                                                                 | Number of on-chain scripts for this dependency                                                      |
| script                    | String                                                                  | Concatenated string of all scripts for this dependency                                              |
| referenceWebsite          | String!                                                                 | Reference website for this dependency (e.g. https://p5js.org)                                       |
| dependencyRegistry        | DependencyRegistry!                                                     | Dependency registry contract that this dependency is registered on                                  |
| updatedAt                 | BigInt!                                                                 | Timestamp of last update                                                                            |

# DependencyRegistry

Description: information about a dependency registry contract

| Field                  | Type                           | Description                                                            |
| ---------------------- | ------------------------------ | ---------------------------------------------------------------------- |
| id                     | Bytes!                         | Unique identifier made up of dependency registry contract address      |
| supportedCoreContracts | [\[Contract!\]!](#contract)    | Core contracts that this registry can provide dependency overrides for |
| dependencies           | [\[Dependency!\]](#dependency) | List of dependencies that are registered on this registry contract     |
| owner                  | Bytes!                         | Current owner of this contract                                         |
| updatedAt              | BigInt!                        | Timestamp of last update                                               |

# DependencyAdditionalCDN

Description: information about an additional CDN for a dependency

| Field      | Type                       | Description                                          |     |
| ---------- | -------------------------- | ---------------------------------------------------- | --- |
| id         | ID!                        | Unique identifier made up of dependency id and index |     |
| dependency | [Dependency!](#dependency) | Dependency this additional CDN belongs to            |     |
| cdn        | String!                    | URL of the CDN                                       |     |
| index      | BigInt!                    | Index of this additional CDN                         |     |

# DependencyAdditionalRepository

Description: information about an additional repository for a dependency

| Field      | Type                       | Description                                          |
| ---------- | -------------------------- | ---------------------------------------------------- |
| id         | ID!                        | Unique identifier made up of dependency id and index |
| dependency | [Dependency!](#dependency) | Dependency this additional repository belongs to     |
| repository | String!                    | URL of the repository                                |
| index      | BigInt!                    | Index of this additional repository                  |

# DependencyScript

Description: information about a script for a dependency

| Field      | Type                       | Description                                              |
| ---------- | -------------------------- | -------------------------------------------------------- |
| id         | ID!                        | Unique identifier made up of dependency id and index     |
| dependency | [Dependency!](#dependency) | Dependency this script belongs to                        |
| index      | BigInt!                    | Index of this script                                     |
| script     | String!                    | Contents of script                                       |
| address    | Bytes!                     | Address of the bytecode storage contract for this script |
