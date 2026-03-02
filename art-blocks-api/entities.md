---
sidebar_position: 2
title: Entities
---

# Entities

This page describes the primary entities available in the Art Blocks GraphQL API and Subgraph. The GraphQL API uses `_metadata` table suffixes (e.g. `projects_metadata` instead of `projects`), while the subgraph uses the base entity names.

!!!info
Only a subset of commonly used entities are documented here. The full schema includes many additional entities such as transfers, receipts, dependencies, external asset dependencies, and more. Explore the complete schema using the [GraphQL API Playground](https://cloud.hasura.io/public/graphiql?endpoint=https://data.artblocks.io/v1/graphql) or the [Subgraph Explorer](https://thegraph.com/explorer/subgraphs/6bR1oVsRUUs6czNiB6W7NNenTXtVfNd5iSiwvS4QbRPB?view=Overview&chain=arbitrum-one).
!!!

- [`projects_metadata`](#projects_metadata)
- [`tokens_metadata`](#tokens_metadata)
- [`contracts_metadata`](#contracts_metadata)
- [`project_minter_configurations`](#project_minter_configurations)
- [`minters_metadata`](#minters_metadata)
- [`minter_filters_metadata`](#minter_filters_metadata)

---

# projects_metadata

Description: Detailed information about Art Blocks projects, including on-chain and off-chain data.

| Field                                         | Type         | Description                                                                                                                   |
| --------------------------------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| id                                            | String!      | Unique identifier made up of contract address and project id (e.g. `0x99a9b7c1116f9ceeb1652de04d5969cce509b069-385`)          |
| project_id                                    | String       | ID of the project on the contract                                                                                             |
| chain_id                                      | Int          | Chain ID of the network the project is deployed on                                                                            |
| contract_address                              | String       | Address of the core contract                                                                                                  |
| name                                          | String       | Project name                                                                                                                  |
| artist_name                                   | String       | Artist name                                                                                                                   |
| artist_address                                | String       | Wallet address of the artist                                                                                                  |
| description                                   | String       | Artist description of the project                                                                                             |
| active                                        | Boolean!     | Determines if the project should be visible to the public                                                                     |
| paused                                        | Boolean!     | Purchases paused                                                                                                              |
| complete                                      | Boolean!     | A project is complete when it has reached its maximum invocations                                                             |
| completed_at                                  | timestamptz  | Timestamp at which the project was completed                                                                                  |
| activated_at                                  | timestamptz  | When project was activated                                                                                                    |
| invocations                                   | bigint!      | Number of times the project has been invoked (number of tokens minted)                                                        |
| max_invocations                               | Int!         | Maximum number of invocations allowed for the project                                                                         |
| price_per_token_in_wei                        | String       | Price per token in wei                                                                                                        |
| currency_symbol                               | String       | Currency symbol for ERC-20 purchases                                                                                          |
| currency_address                              | String       | ERC-20 contract address if the project is purchasable via ERC-20                                                              |
| license                                       | String       | License for the project                                                                                                       |
| script                                        | String       | The full project script                                                                                                       |
| script_count                                  | bigint       | The number of scripts stored on-chain                                                                                         |
| script_json                                   | jsonb        | Extra information about the script and rendering options                                                                      |
| script_type_and_version                       | String       | Script type and version (e.g. `p5js@1.0.0`)                                                                                  |
| aspect_ratio                                  | numeric      | Aspect ratio of the project                                                                                                   |
| locked                                        | Boolean      | Once the project is locked its script may never be updated again                                                              |
| website                                       | String       | Artist or project website                                                                                                     |
| base_uri                                      | String       | The base URI for token metadata                                                                                               |
| royalty_percentage                             | Int          | Artist/additional payee royalty percentage                                                                                    |
| additional_payee                               | String       | Address to split primary sales with the artist                                                                                |
| additional_payee_percentage                    | Int          | Percentage of artist's share of primary sales to additional payee                                                             |
| additional_payee_secondary_sales_address       | String       | Address to split secondary sales with the artist                                                                              |
| additional_payee_secondary_sales_percentage    | Int          | Percentage of artist's share of secondary sales to additional payee                                                           |
| render_provider_secondary_sales_address        | String       | Address for render provider secondary sales                                                                                   |
| render_provider_secondary_sales_bps            | Int          | Basis points for render provider secondary sales                                                                              |
| engine_platform_provider_secondary_sales_address | String     | Address for engine platform provider secondary sales                                                                          |
| engine_platform_provider_secondary_sales_bps   | Int          | Basis points for engine platform provider secondary sales                                                                     |
| external_asset_dependency_count                | bigint       | The number of external asset dependencies stored on-chain                                                                     |
| external_asset_dependencies_locked             | Boolean!     | Once external asset dependencies are locked they may never be modified again                                                  |
| is_artblocks                                   | Boolean      | Whether the project is an Art Blocks flagship project                                                                         |
| vertical_name                                  | String       | The vertical (category) this project belongs to                                                                               |
| slug                                           | String       | URL slug for the project                                                                                                      |
| series_id                                      | Int          | Series this project belongs to                                                                                                |
| render_delay                                   | Int          | Render delay in seconds before capturing a static image                                                                       |
| canvas_mode                                    | Boolean      | Whether the project uses canvas mode                                                                                          |
| lowest_listing                                 | float8       | Lowest current listing price                                                                                                  |
| created_at                                     | BigInt!      | When project was created                                                                                                      |
| updated_at                                     | timestamp    | When project was last updated                                                                                                 |

### Relationships

| Field                                  | Related Entity                  | Description                                          |
| -------------------------------------- | ------------------------------- | ---------------------------------------------------- |
| contract                               | contracts_metadata              | Contract associated with this project                |
| tokens                                 | tokens_metadata                 | Tokens minted from this project                      |
| artist                                 | users                           | Artist account                                       |
| minter_configuration                   | project_minter_configurations   | Current minter configuration for this project        |
| features                               | projects_features               | Computed feature fields for this project             |
| series                                 | project_series                  | Series this project belongs to                       |
| vertical                               | project_verticals               | Vertical/category of this project                    |

---

# tokens_metadata

Description: Information about individual Art Blocks tokens.

| Field                | Type        | Description                                                           |
| -------------------- | ----------- | --------------------------------------------------------------------- |
| id                   | String!     | Unique identifier made up of contract address and token id            |
| token_id             | String      | ID of the token on the contract                                       |
| chain_id             | Int         | Chain ID of the network the token is on                               |
| contract_address     | String      | Address of the core contract                                          |
| project_id           | String      | ID of the project this token belongs to                               |
| project_name         | String      | Name of the project this token belongs to                             |
| invocation           | Int         | Invocation number within the project                                  |
| hash                 | String      | Unique string used as input to the token's project script             |
| owner_address        | String      | Current owner of the token                                            |
| minted_at            | timestamptz | When the token was minted                                             |
| mint_transaction_hash| String      | Transaction hash of token mint                                        |
| features             | jsonb       | Computed feature data for this token                                  |
| live_view_url        | String      | URL to the live generator view for this token                         |
| live_view_path       | String      | Path portion of the live view URL                                     |
| media_url            | String      | URL to the static media snapshot                                      |
| preview_asset_url    | String      | URL to the preview asset                                              |
| primary_asset_url    | String      | URL to the primary asset                                              |
| last_transferred_at  | timestamptz | When the token was last transferred                                   |
| updated_at           | timestamp   | When the token record was last updated                                |

### Relationships

| Field                    | Related Entity     | Description                          |
| ------------------------ | ------------------ | ------------------------------------ |
| contract                 | contracts_metadata | Contract the token is on             |
| project                  | projects_metadata  | Project the token belongs to         |
| owner                    | users              | Current owner account                |
| image                    | media              | Standard image render                |
| high_res_image           | media              | High resolution image render         |
| low_res_image            | media              | Low resolution / thumbnail render    |
| video                    | media              | Video render                         |

---

# contracts_metadata

Description: Information about Art Blocks core contracts.

| Field                                             | Type     | Description                                                                                 |
| ------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------- |
| address                                           | String!  | Contract address                                                                            |
| chain_id                                          | Int      | Chain ID of the network the contract is deployed on                                         |
| name                                              | String   | Contract name                                                                               |
| core_version                                      | String   | Core contract version                                                                       |
| admin                                             | String   | Admin address                                                                               |
| render_provider_address                           | String   | Address that receives primary sales platform fees                                           |
| render_provider_percentage                        | Int      | Percentage of primary sales allocated to the platform                                       |
| default_render_provider_secondary_sales_address   | String   | Address that receives secondary sales platform royalties                                    |
| default_render_provider_secondary_sales_bps       | Int      | Basis points of secondary sales allocated to the platform                                   |
| minter_filter_address                             | String   | Address of the associated minter filter                                                     |
| dependency_registry_address                       | String   | Address of the dependency registry contract                                                 |
| preferred_ipfs_gateway                            | String   | Preferred IPFS gateway (Engine Flex)                                                        |
| preferred_arweave_gateway                         | String   | Preferred Arweave gateway (Engine Flex)                                                     |
| new_projects_forbidden                            | Boolean! | Whether new projects are forbidden on this contract                                         |
| token_base_url                                    | String   | Base URL for token metadata                                                                 |
| updated_at                                        | timestamp| When the contract record was last updated                                                   |

### Relationships

| Field               | Related Entity           | Description                                    |
| ------------------- | ------------------------ | ---------------------------------------------- |
| projects            | projects_metadata        | Projects on this contract                      |
| minter_filter       | minter_filters_metadata  | Associated minter filter                       |
| partner             | partners                 | Associated partner                             |
| type                | contract_types           | Contract type                                  |

---

# project_minter_configurations

Description: Minting configuration for a specific project, as configured by the artist.

| Field                       | Type     | Description                                                                              |
| --------------------------- | -------- | ---------------------------------------------------------------------------------------- |
| id                          | String!  | Unique identifier                                                                        |
| project_id                  | String   | Associated project ID                                                                    |
| minter_id                   | String   | Associated minter ID                                                                     |
| chain_id                    | Int      | Chain ID                                                                                 |
| price_is_configured         | Boolean! | Whether the token price has been configured                                              |
| currency_symbol             | String   | Currency symbol — ETH reserved for ether                                                 |
| currency_address            | String   | Currency address — address(0) reserved for ether                                         |
| base_price                  | String   | Price of token or resting price of Dutch auction, in wei                                 |
| max_invocations             | Int      | Maximum number of invocations allowed on the minter                                      |
| purchase_to_disabled        | Boolean  | Whether purchasing to another address is disabled                                        |
| auction_start_time          | timestamptz | Auction start time (for auction minters)                                              |
| auction_end_time            | timestamptz | Auction end time (for auction minters)                                                |
| extra_minter_details        | jsonb    | Additional minter-specific configuration (e.g. Dutch auction parameters)                 |
| offchain_extra_minter_details | jsonb  | Off-chain minter-specific configuration details                                          |

### Relationships

| Field   | Related Entity    | Description            |
| ------- | ----------------- | ---------------------- |
| project | projects_metadata | The associated project |
| minter  | minters_metadata  | The associated minter  |

---

# minters_metadata

Description: Information about minter contracts.

| Field                                    | Type     | Description                                                     |
| ---------------------------------------- | -------- | --------------------------------------------------------------- |
| address                                  | String!  | Minter contract address                                         |
| chain_id                                 | Int      | Chain ID                                                        |
| minter_filter_address                    | String   | Address of the associated minter filter                         |
| is_globally_allowlisted_on_minter_filter | Boolean  | Whether the minter is globally allowed on its minter filter     |
| extra_minter_details                     | jsonb    | Configuration details specific to this minter type (json)       |

### Relationships

| Field         | Related Entity          | Description                 |
| ------------- | ----------------------- | --------------------------- |
| minter_filter | minter_filters_metadata | Associated minter filter    |
| type          | minter_types            | Minter type classification  |

---

# minter_filters_metadata

Description: Information about minter filter contracts, which manage the set of approved minters for a contract or set of contracts.

| Field                  | Type   | Description                                  |
| ---------------------- | ------ | -------------------------------------------- |
| address                | String!| Minter filter contract address               |
| chain_id               | Int    | Chain ID                                     |
| core_registry_address  | String | Associated core registry contract address    |
