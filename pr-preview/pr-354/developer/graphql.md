# GraphQL Reference

The Art Blocks GraphQL API and Subgraph provide structured access to on-chain and off-chain data. This page covers the primary entities, their fields, and example queries for both the Hasura API and the Subgraph.

**API Playground (Hasura):** [https://cloud.hasura.io/public/graphiql?endpoint=https://data.artblocks.io/v1/graphql](https://cloud.hasura.io/public/graphiql?endpoint=https://data.artblocks.io/v1/graphql)

!!!info
For AI-assisted querying, the [Art Blocks MCP Server](/developer/mcp-server/quick-start/) provides `explore_table`, `build_query`, and `graphql_query` tools that validate field names, handle chain filtering, and construct queries interactively.
!!!

---

## Which API to Use

**Hasura GraphQL API** (`data.artblocks.io`) — recommended for most integrations. Provides on-chain + off-chain data including media URLs, minter configuration, descriptions, and project metadata. Uses `_metadata` table suffixes.

**Subgraph** (The Graph) — useful for on-chain-only data and integrations that require decentralized infrastructure. Uses camelCase field names.

---

## Primary Entities

### `projects_metadata`

Detailed information about Art Blocks projects, including on-chain and off-chain data.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | String! | `<contract_address>-<project_id>` |
| `project_id` | String | Project ID on the contract |
| `chain_id` | Int | Chain ID |
| `contract_address` | String | Core contract address |
| `name` | String | Project name |
| `artist_name` | String | Artist name |
| `artist_address` | String | Artist wallet address |
| `description` | String | Project description |
| `active` | Boolean! | Whether the project is publicly visible |
| `paused` | Boolean! | Whether purchases are paused |
| `complete` | Boolean! | Whether the project has reached max invocations |
| `completed_at` | timestamptz | When the project sold out |
| `activated_at` | timestamptz | When the project was activated |
| `invocations` | bigint! | Number of tokens minted |
| `max_invocations` | Int! | Maximum supply |
| `script` | String | Full project script |
| `script_type_and_version` | String | E.g. `p5js@1.0.0` |
| `aspect_ratio` | numeric | Artwork aspect ratio |
| `locked` | Boolean | Whether the script is permanently locked |
| `website` | String | Artist or project website |
| `license` | String | Project license |
| `lowest_listing` | float8 | Current lowest secondary listing price |
| `vertical_name` | String | Category (curated, presents, studio, etc.) |
| `is_artblocks` | Boolean | Whether it's an Art Blocks flagship project |
| `slug` | String | URL slug |
| `render_delay` | Int | Seconds before static capture |

**Key relationships:** `contract`, `tokens`, `artist`, `minter_configuration`, `features`, `tags`, `vertical`

---

### `tokens_metadata`

Information about individual tokens.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | String! | `<contract_address>-<token_id>` |
| `token_id` | String | Token ID |
| `chain_id` | Int | Chain ID |
| `contract_address` | String | Core contract address |
| `project_id` | String | Associated project ID |
| `invocation` | Int | Invocation number within the project |
| `hash` | String | Token hash (used as PRNG seed) |
| `owner_address` | String | Current owner |
| `minted_at` | timestamptz | Mint timestamp |
| `features` | jsonb | Computed trait data |
| `live_view_url` | String | Generator URL for live artwork |
| `media_url` | String | Media proxy URL for static image |
| `primary_asset_url` | String | Primary asset URL |
| `preview_asset_url` | String | Thumbnail URL |

**Key relationships:** `contract`, `project`, `owner`, `image`

---

### `contracts_metadata`

Information about Art Blocks core contracts.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `address` | String! | Contract address |
| `chain_id` | Int | Chain ID |
| `name` | String | Contract name |
| `core_version` | String | Core contract version |
| `admin` | String | Admin address |
| `minter_filter_address` | String | Associated minter filter |
| `dependency_registry_address` | String | Dependency registry address |
| `preferred_ipfs_gateway` | String | Preferred IPFS gateway (Flex) |
| `preferred_arweave_gateway` | String | Preferred Arweave gateway (Flex) |

---

### `project_minter_configurations`

Minting configuration for a project.

| Field | Type | Description |
| ----- | ---- | ----------- |
| `price_is_configured` | Boolean! | Whether price has been set |
| `currency_symbol` | String | Currency (ETH or ERC-20 symbol) |
| `base_price` | String | Price in wei |
| `max_invocations` | Int | Minter-level max invocations |
| `auction_start_time` | timestamptz | Auction start (for auction minters) |
| `auction_end_time` | timestamptz | Auction end (for auction minters) |
| `extra_minter_details` | jsonb | Minter-specific config (see below) |

The `extra_minter_details` field is a JSONB object with minter-specific fields. For a Dutch Auction minter:

```json
{
  "startTime": 1676052000,
  "halfLifeSeconds": 315,
  "approximateDAExpEndTime": 1676053820,
  "startPrice": "11000000000000000000",
  "currentSettledPrice": "557638888888888889",
  "auctionRevenuesCollected": true,
  "numSettleableInvocations": 172
}
```

---

## Example Queries

### Hasura API Examples

Always include `chain_id` in Hasura queries to scope to a specific network.

**Get a project by ID on Ethereum:**

```graphql
{
  projects_metadata(
    where: {
      id: { _eq: "0x99a9b7c1116f9ceeb1652de04d5969cce509b069-385" }
      chain_id: { _eq: 1 }
    }
  ) {
    id
    name
    artist_name
    invocations
    max_invocations
  }
}
```

**Get a token with project info:**

```graphql
{
  tokens_metadata(
    where: {
      id: { _eq: "0x99a9b7c1116f9ceeb1652de04d5969cce509b069-385000000" }
      chain_id: { _eq: 1 }
    }
  ) {
    id
    token_id
    hash
    owner_address
    live_view_url
    media_url
    features
    project {
      name
      artist_name
    }
  }
}
```

**Get recently activated flagship projects on Ethereum:**

```graphql
{
  projects_metadata(
    where: { is_artblocks: { _eq: true }, chain_id: { _eq: 1 } }
    order_by: { activated_at: desc }
    limit: 5
  ) {
    id
    name
    artist_name
    invocations
    max_invocations
  }
}
```

**Get minter configuration for a project:**

```graphql
{
  projects_metadata(
    where: {
      id: { _eq: "0x99a9b7c1116f9ceeb1652de04d5969cce509b069-385" }
      chain_id: { _eq: 1 }
    }
  ) {
    name
    minter_configuration {
      price_is_configured
      currency_symbol
      base_price
      extra_minter_details
      minter {
        address
        type {
          label
        }
      }
    }
  }
}
```

---

### Subgraph Examples

The Subgraph uses camelCase field names and the base entity names (without `_metadata` suffix).

**Get a project by short ID:**

```graphql
{
  projects(
    where: {
      projectId: "385"
      contract_in: ["0x99a9b7c1116f9ceeb1652de04d5969cce509b069"]
    }
  ) {
    id
    invocations
    artistName
    name
  }
}
```

**Get the 5 most recently created projects:**

```graphql
{
  projects(first: 5, orderBy: createdAt, orderDirection: desc) {
    id
    name
    artistName
    invocations
    maxInvocations
  }
}
```

**Get the top 10 projects by invocations:**

```graphql
{
  projects(first: 10, orderBy: invocations, orderDirection: desc) {
    id
    name
    artistName
    invocations
    maxInvocations
  }
}
```

**Get all tokens owned by an address:**

```graphql
{
  tokens(where: { owner: "<owner-address>" }) {
    id
    tokenId
    project {
      name
      artistName
    }
  }
}
```

**Get the script for a project:**

```graphql
{
  project(id: "0x059edd72cd353df5106d2b9cc5ab83a52287ac3a-0") {
    script
  }
}
```

---

## Advanced GraphQL (MCP Tools)

The [Art Blocks MCP Server](/developer/mcp-server/advanced-graphql/) includes six GraphQL tools for custom queries:

| Tool | Purpose |
|---|---|
| `explore_table` | Inspect a table's fields, types, and relationships |
| `validate_fields` | Check whether specific fields exist on a table |
| `build_query` | Build a validated GraphQL query with WHERE filters |
| `query_optimizer` | Rewrite queries to use `*_metadata` tables |
| `graphql_query` | Execute a raw GraphQL query |
| `graphql_introspection` | Full schema introspection |

---

## Pagination

The Graph enforces limits: `first <= 1000` and `skip <= 5000`. For large result sets, paginate using a cursor-style approach based on an attribute like token ID or block number rather than high `skip` values. See the [Graph documentation](https://thegraph.com/docs/en/developer/graphql-api/#pagination) for guidance.
