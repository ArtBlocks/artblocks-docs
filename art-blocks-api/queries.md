---
sidebar_position: 3
title: Querying
---

# Querying

Below are some sample queries you can use to gather information from the Art Blocks contracts.

You can build your own queries using a [GraphQL Explorer](https://graphiql-online.com/graphiql) and enter your endpoint to limit the data to exactly what you need.

## Subgraph Querying Walkthrough

The following provides some examples of how to use the Art Blocks subgraph to perform common queries.

# The Basics

Retrieving a specific Art Blocks project by short ID (no contract):

<table>
<tr>
<td> Network </td> <td> Contract Type </td> <td style="width:700px"> Query </td>
</tr>
<tr>
<td> Mainnet </td> <td> Flagship </td>
<td>

```graphql
{
  projects(
    where: {
      projectId: "0"
      contract_in: [
        "0x059edd72cd353df5106d2b9cc5ab83a52287ac3a"
        "0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270"
      ]
    }
  ) {
    id
    invocations
    artistName
    name
  }
}
```

</td>
</tr>
<tr>
<td> Mainnet </td> <td> Engine </td>
<td>

```graphql
{
  projects(
    where: {
      projectId: "1"
      contract_in: ["0x0a1bbd57033f57e7b6743621b79fcb9eb2ce3676"]
    }
  ) {
    id
    invocations
    artistName
    name
  }
}
```

</td>
</tr>
</table>

Retrieving a specific Art Blocks project by full ID (includes contract):

<table>
<tr>
<td> Network </td> <td> Contract Type </td> <td style="width:600px"> Query </td>
</tr>
<tr>
<td> Mainnet </td> <td> Flagship </td>
<td>

```graphql
{
  project(id: "0x059edd72cd353df5106d2b9cc5ab83a52287ac3a-0") {
    id
    invocations
    artistName
    name
  }
}
```

</td>
</tr>
<tr>
<td> Mainnet </td> <td> Engine </td>
<td>

```graphql
{
  project(id: "0x0a1bbd57033f57e7b6743621b79fcb9eb2ce3676-1") {
    id
    invocations
    artistName
    name
  }
}
```

</td>
</tr>
</table>

---

<br>
<br>
<br>

Retrieving a specific Art Blocks token by short ID (no contract):

<table>
<tr>
<td> Network </td> <td> Contract Type </td> <td style="width:700px"> Query </td>
</tr>
<tr>
<td> Mainnet </td> <td> Flagship </td>
<td>

```graphql
{
  tokens(
    where: {
      tokenId: "0"
      contract_in: [
        "0x059edd72cd353df5106d2b9cc5ab83a52287ac3a"
        "0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270"
      ]
    }
  ) {
    id
    tokenId
  }
}
```

</td>
</tr>
<tr>
<td> Mainnet </td> <td> Engine </td>
<td>
Requires full ID (includes contract)
</td>
</tr>
</table>

---

<br>
<br>
<br>

Retrieving a specific Art Blocks token by full ID (includes contract):

<table>
<tr>
<td> Network </td> <td> Contract Type </td> <td style="width:600px"> Query </td>
</tr>
<tr>
<td> Mainnet </td> <td> Flagship </td>
<td>

```graphql
{
  token(id: "0x059edd72cd353df5106d2b9cc5ab83a52287ac3a-0") {
    id
    tokenId
  }
}
```

</td>
</tr>
<tr>
<td> Mainnet </td> <td> Engine </td>
<td>

```graphql
{
  token(id: "0x0a1bbd57033f57e7b6743621b79fcb9eb2ce3676-1000000") {
    id
    tokenId
  }
}
```

</td>
</tr>
</table>

---

<br>
<br>
<br>

# Beyond The Basics

Retrieve the last 5 most recently created projects across Art Blocks and Engine (use a `contract_in` filter to restrict to specific contracts):

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

Retrieve the top 10 projects across Art Blocks and Engine, based on # of invocations:

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

Retrieve the most recently minted Art Blocks token:

```graphql
{
  tokens(
    first: 1
    orderBy: createdAt
    orderDirection: desc
    where: {
      contract_in: [
        "0x059edd72cd353df5106d2b9cc5ab83a52287ac3a"
        "0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270"
      ]
    }
  ) {
    id
    hash
    owner {
      id
    }
    project {
      name
      artistName
    }
  }
}
```

Retrieve all tokens owned by a specific address:

```graphql
{
  tokens(where: { owner: "<owner address>" }) {
    id
  }
}
```

Retrieve the general metadata/status for the Art Blocks subgraph (useful for debugging):

```graphql
{
  _meta {
    hasIndexingErrors
    block {
      number
      hash
    }
  }
}
```

Retrieve the project script for a given project id:

```graphql
{
  project(id: "0x059edd72cd353df5106d2b9cc5ab83a52287ac3a-0") {
    script
  }
}
```

Pagination should be used for large queries. The Graph enforces upper limits on `first` and `skip` parameters since they generally perform poorly when set to large values (limits as of 01/2022 are `first<=1000` and `skip<=5000`). It is much better to page through entities based on an attribute such as token ID, block number, or some other parameter. For more information, see [The Graph documentation](https://thegraph.com/docs/en/developer/graphql-api/#pagination).

# Project Info

Pull all projects and return their name, as well as additional data:

```graphql
{
  projects(
    where: {
      contract_in: [
        "0x059edd72cd353df5106d2b9cc5ab83a52287ac3a"
        "0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270"
      ]
    }
    first: 500
  ) {
    projectId
    name
    invocations
    artistName
  }
}
```

Get all the wallet owners of a project (replace PROJECT with the project name):

```graphql
{
  projects(where: { name: "PROJECT" }) {
    id
    artistAddress
    additionalPayee
  }
}
```

Get the addresses of anyone that owns a mint from a project:

```graphql
{
  projects(where: { name: "PROJECT" }) {
    owners {
      id
      count
    }
  }
}
```

Get the transaction hash for Chromie Squiggle #0:

```graphql
{
  tokens(
    where: {
      tokenId: "0"
      contract: "0x059edd72cd353df5106d2b9cc5ab83a52287ac3a"
    }
  ) {
    id
    tokenId
    transactionHash
    project {
      name
    }
  }
}
```

---

# GraphQL API Queries

The Art Blocks GraphQL API (Hasura) uses `_metadata` table suffixes and a slightly different naming convention (snake_case) compared to the subgraph (camelCase). Below are equivalent examples using the GraphQL API.

Since the GraphQL API is multichain, we recommend always including `chain_id` in your `where` clauses to scope queries to a specific network. Supported chain IDs: `1` (Ethereum), `42161` (Arbitrum), `8453` (Base).

Retrieve a project by its full ID on Ethereum mainnet:

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
    chain_id
    contract_address
  }
}
```

Retrieve a token with its project info on Ethereum mainnet:

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
    chain_id
    hash
    owner_address
    live_view_url
    media_url
    project {
      name
      artist_name
    }
  }
}
```

Retrieve the most recent Art Blocks flagship projects on Ethereum mainnet:

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
    chain_id
  }
}
```

Retrieve minter configuration for a project on Ethereum mainnet (useful for displaying purchase information):

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
    minter_configuration {
      price_is_configured
      currency_symbol
      currency_address
      base_price
      max_invocations
      extra_minter_details
      minter {
        address
        extra_minter_details
        type {
          label
        }
      }
    }
  }
}
```

The `extra_minter_details` field contains a JSONB object with minter-specific configuration. For example, a Dutch Auction minter may include:

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
