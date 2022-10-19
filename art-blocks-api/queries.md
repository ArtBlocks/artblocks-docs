---
sidebar_position: 3
title: Querying and API Overview

---

# Querying and API Overview

Below are some sample queries you can use to gather information from the Artblocks contracts.

You can build your own queries using a [GraphQL Explorer](https://graphiql-online.com/graphiql) and enter your endpoint to limit the data to exactly what you need.

!!!
We are currently in the process of working on finalizing a more comprehensive project-oriented API. This API will encapsulate both onchain data (the information readily available via the Art Blocks public subgraph on The Graph) and additional off-chain data (e.g., all available features for a given project)
!!!

## Hosted APIs

As a quick overview, the main APIs that exist currently are:

### Token API

Provides the token metadata for a given Art Blocks token.

Pattern: `https:token.artblocks.io/{tokenID}`\
Sample: https://token.artblocks.io/0

## Subgraph Querying Walkthrough

The following provides some examples on how to use the Art Blocks subgraph to perform a handful of common queries.

#### Important Notes

- Performance/indexing on the hosted subgraph service is oftentimes slower compared to the decentralized subgraph. That being said, the hosted subgraph is free while the decentralized one requires pay-per-query in GRT.
- The Art Blocks subgraphs currently also index any PBAB (Powered by Artblocks) contracts, in addition to the core Art Blocks contracts. Please keep that in mind and make use of the `contract_in` filter to ensure you are working with Art Blocks data only, if that is your intention.
- While querying against the subgraph if using the `contract_in` filter the Art Blocks contracts to restrict for are `0x059edd72cd353df5106d2b9cc5ab83a52287ac3a` (for the V0 contract that supports projects 0-3) and `0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270` (for the V1 contract that supports projects 4-current).

# The Basics

Retrieving a specific Art Blocks project by short ID (no contract):

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

Retrieving a specific Art Blocks project by full ID (includes contract):

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

Retrieving a specific Art Blocks token by short ID (no contract):

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

Retrieving a specific Art Blocks token by full ID (includes contract):

```graphql
{
  token(id: "0x059edd72cd353df5106d2b9cc5ab83a52287ac3a-0") {
    id
    tokenId
  }
}
```

# Beyond The Basics

Retrieve the last 5 most recently created projects across Art Blocks and Powered by Art Blocks (remember that you can use a `contract_in` filter to restrict this to only specific contracts):

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

Retrieve the top 10 projects across Art Blocks and Powered by Art Blocks, based on # of invocations:

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

Retrieve all tokens owned by a specific address, across Art Blocks and Powered by Art Blocks:

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

Retrieve the project script for a given project id

```graphql
{
  project(id: "0x059edd72cd353df5106d2b9cc5ab83a52287ac3a-0") {
    script
  }
}
```

Pagination should be used for large queries. The Graph enforces upper limits on `first` and `skip` parameters since they generally perform poorly when set to large values (limits as of 01/2022 are `first<=1000` and `skip<=5000`). It is much better to page through entities based on an attribute such as token ID, block number, or some other parameter. For more information, see [The Graph documentation](https://thegraph.com/docs/en/developer/graphql-api/#pagination)

# Project info

- pull all projects and get their name, as well as lots of additional data:

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

- get all the wallet owners of a project (Replace PROJECT with the project name you are looking for)

```graphql
{
  projects(where: { name: "PROJECT" }) {
    id
    artistAddress
    additionalPayee
  }
}
```

- If you're looking for the addresses of anyone that owns a mint from a project

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

- get that txnhash for squiggle 0, you could run the following query on the AB subgraph playground

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
