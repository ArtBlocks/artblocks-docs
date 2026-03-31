---
order: 600
description: Advanced GraphQL tools for custom queries against the Art Blocks data layer.
---

# Advanced GraphQL

The MCP server includes 6 GraphQL tools for direct access to the Art Blocks Hasura API. Most users will never need these — the [domain-specific tools](/developer/mcp-server/capabilities/) cover common use cases. Use GraphQL for custom aggregations, sales history, cross-table joins, or any query not handled by the higher-level tools.

---

## Tools

| Tool | Purpose |
|------|---------|
| `explore_table` | Inspect a table's fields, types, and relationships. Returns a curated shortlist for well-known tables (`projects_metadata`, `tokens_metadata`) or the full schema dump. |
| `validate_fields` | Check whether specific fields exist on a table before writing a query. Faster than full introspection. |
| `build_query` | Build a validated GraphQL query with field validation, WHERE filters, and suggestions. The safest way to start. |
| `query_optimizer` | Rewrite a query to use preferred `*_metadata` tables (e.g., `projects_metadata` instead of `projects`). |
| `graphql_query` | Execute a raw GraphQL query against the Art Blocks Hasura endpoint. Pass `chainId` to make `$chainId` available as a variable. |
| `graphql_introspection` | Full GraphQL schema introspection. Returns all types, fields, and relationships. |

---

## Recommended Workflow

```
explore_table  →  build_query  →  graphql_query
```

1. **Discover the schema** — Call `explore_table` with the table you want to query. For `projects_metadata` and `tokens_metadata`, it returns a curated shortlist of the most useful fields organized by category, plus key relationships with suggested subfields. Pass `showAllFields: true` for the full schema dump.

2. **Build a validated query** — Call `build_query` with your desired fields and filters. It validates field names, adds suggestions for typos, and returns a ready-to-execute GraphQL query.

3. **Execute** — Call `graphql_query` with the generated query. Pass `chainId` if your query needs chain filtering.

If you already know the schema, skip straight to `build_query` or `graphql_query`.

---

## Key Tables

Always use the `_metadata` table variants — they include richer joined data and are optimized for read access.

| Use this | Not this |
|----------|----------|
| `projects_metadata` | `projects` |
| `tokens_metadata` | `tokens` |
| `contracts_metadata` | `contracts` |

`query_optimizer` automatically rewrites queries that reference the non-metadata variants.

### projects_metadata — Common Fields

| Category | Fields |
|----------|--------|
| **Identity** | `id`, `project_id`, `chain_id`, `contract_address`, `slug`, `name`, `artist_name`, `artist_address`, `description`, `website`, `license` |
| **Status and Supply** | `active`, `paused`, `complete`, `completed_at`, `locked`, `start_datetime`, `invocations`, `max_invocations` |
| **Classification** | `vertical_name`, `heritage_curation_status`, `is_artblocks` |
| **Media** | `aspect_ratio`, `preview_render_type`, `script_type_and_version` |
| **Market** | `lowest_listing` |

Key relationships: `vertical`, `minter_configuration`, `featured_token`, `contract`, `artist_profiles`, `tags`

### tokens_metadata — Common Fields

| Category | Fields |
|----------|--------|
| **Identity** | `id`, `token_id`, `chain_id`, `contract_address`, `project_id`, `invocation`, `hash` |
| **Ownership** | `owner_address`, `minted_at`, `last_transferred_at` |
| **Media** | `media_url`, `primary_asset_url`, `preview_asset_url` |
| **Features** | `features` (JSON object of token traits) |
| **Listing** | `list_price`, `list_currency_symbol`, `list_platform` |

Key relationships: `project`, `image`

---

## Chain IDs

| Chain | ID |
|-------|----|
| Ethereum mainnet | `1` (default) |
| Arbitrum | `42161` |
| Base | `8453` |

Pass `chainId` to `graphql_query` to make `$chainId` available as a variable in your query. Always filter by chain when querying multi-chain data to avoid cross-chain noise.

---

## Example Queries

These examples show queries that require raw GraphQL — things the domain-specific tools don't cover.

### Recent secondary sales

```graphql
query {
  purchases_metadata(
    order_by: { block_timestamp: desc }
    limit: 20
    where: { chain_id: { _eq: 1 } }
  ) {
    token_id
    price_in_eth
    block_timestamp
    buyer_address
    seller_address
  }
}
```

### Unique collectors for a project

```graphql
# Fidenza by Tyler Hobbs (project 78 on Art Blocks V1 contract)
query {
  tokens_metadata_aggregate(
    where: {
      project_id: { _eq: "0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270-78" }
    }
    distinct_on: owner_address
  ) {
    aggregate {
      count
    }
  }
}
```

### All tokens in a project (with features)

```graphql
# Chromie Squiggle by Snowfro (project 0 on Art Blocks V1 contract)
query {
  tokens_metadata(
    where: {
      project_id: { _eq: "0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270-0" }
    }
    order_by: { invocation: asc }
    limit: 50
  ) {
    token_id
    invocation
    owner_address
    features
  }
}
```

### Projects using a specific script type

```graphql
query {
  projects_metadata(
    where: {
      script_type_and_version: { _ilike: "%three%" }
      chain_id: { _eq: 1 }
      complete: { _eq: false }
    }
    limit: 20
  ) {
    id
    name
    artist_name
    script_type_and_version
    invocations
    max_invocations
  }
}
```

---

## Tips

- Use `explore_table` to understand fields and relationships before writing a query — the curated view is much easier to scan than the full schema dump
- `build_query` is the safest starting point — it validates fields and suggests corrections for typos
- For unknown fields, `validate_fields` is faster than running a full `graphql_introspection`
- Always pass `chainId` when querying multi-chain data
- The `id` field on projects follows the format `<contract_address>-<project_index>` and on tokens follows `<contract_address>-<token_number>`
