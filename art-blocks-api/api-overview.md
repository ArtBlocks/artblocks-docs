# API Overview

An overview of the current Art Blocks APIs.

!!!
We are currently in the process of working on finalizing a more comprehensive project-oriented API which we plan to release in the first half of 2022. This API will encapsulate both onchain data (the information readily available via the Art Blocks public subgraph on The Graph) and additional off-chain data (e.g., all available features for a given project)
!!!

## Hosted APIs

As a quick overview, the main APIs that exist currently are:

### Token API

Provides the token metadata for a given Art Blocks token.

Pattern: `https:token.artblocks.io/{tokenID}`\
Sample: https://token.artblocks.io/0

### Generator API

Provides an i-frame-able live-view for the art associated with a given Art Blocks token.

Pattern: `https://generator.artblocks.io/{tokenID}`\
Sample: https://generator.artblocks.io/0

### Media API/Media server

Provides a static snapshot of the rendered live-view for a given Art Blocks token.

Pattern: `https://media.artblocks.io/{tokenID}.png`\
Sample: https://media.artblocks.io/0.png

---

In addition to the standard static renders provided for each token, there are two other static renders currently provided: "HD" and "thumbnail". These items can be found at:

* HD Renders – `https://media.artblocks.io/hd/{tokenID}.png`
* Thumbnail Renders – `https://media.artblocks.io/thumb/{tokenID}.png`

Please note that these additional static render formats are still currently being back-filled and may not yet be present for all tokens. Our current recommendation for those looking to depend on the "HD" or "thumbnail" responses is to a) first attempt the HD/thumb image resource that you would pefer, b) if this resource is not available, fall back to the standard sized image resource.

Please also note that the Generator API and Media API links for a given token are included in the token response for that token from the Token API.

## Art Blocks Subgraph (via The Graph)

The Art Blocks mainnet subgraph on The Graph can currently be queried against via both hosted service (https://thegraph.com/hosted-service/subgraph/artblocks/art-blocks) and via the decentralized Graph network (https://thegraph.com/explorer/subgraph?id=0x3c3cab03c83e48e2e773ef5fc86f52ad2b15a5b0-0).

**Recommandation:** Using the above links, familiarize yourself with the subgraph’s schema, via the GraphQL playground.

### Subgraph Querying Walkthrough

The following provides some examples on how to use the Art Blocks subgraph to perform a handful of common queries.

#### Important Notes

* Performance/indexing on the hosted subgraph service is oftentimes slower compared to the decentralized subgraph. That being said, the hosted subgraph is free while the decentralized one requires pay-per-query in GRT.
* The Art Blocks subgraphs currently also index any PBAB (Powered by Artblocks) contracts, in addition to the core Art Blocks contracts. Please keep that in mind and make use of the `contract_in` filter to ensure you are working with Art Blocks data only, if that is your intention.
* While querying against the subgraph if using the `contract_in` filter the Art Blocks contracts to restrict for are `0x059edd72cd353df5106d2b9cc5ab83a52287ac3a` (for the V0 contract that supports projects 0-3) and `0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270` (for the V1 contract that supports projects 4-current).

#### The Basics

Retrieving a specific Art Blocks project by short ID (no contract):

```graphql
{
  projects(where: {projectId: "0", contract_in: ["0x059edd72cd353df5106d2b9cc5ab83a52287ac3a", "0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270"]}) {
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
  project(id:"0x059edd72cd353df5106d2b9cc5ab83a52287ac3a-0") {
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
  tokens(where: {tokenId: "0", contract_in: ["0x059edd72cd353df5106d2b9cc5ab83a52287ac3a", "0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270"]}) {
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

#### Beyond The Basics

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
  tokens(first: 1, orderBy: createdAt, orderDirection: desc, where:{ contract_in: ["0x059edd72cd353df5106d2b9cc5ab83a52287ac3a", "0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270"]}) {
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
  tokens(where: {owner: "<owner address>"}) {
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

Pagination should be used for large queries. The Graph enforces upper limits on `first` and `skip` parameters since they generally perform poorly when set to large values (limits as of 01/2022 are `first<=1000` and `skip<=5000`). It is much better to page through entities based on an attribute such as token ID, block number, or some other parameter. For more information, see [The Graph documentation](https://thegraph.com/docs/en/developer/graphql-api/#pagination)
