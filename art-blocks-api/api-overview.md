# API Overview

An overview of the current Art Blocks APIs.

!!!
We are currently in the process of working on finalizing a more comprehensive project-oriented API which we plan to release in the first half of 2022. This API will encapsulate both onchain data (the information readily available via the Art Blocks public subgraph on The Graph) and additional off-chain data (e.g., all available features for a given project)
!!!

Quick Links:
- [Token API](#Token-API)
- [Generator API](#Generator-API)
- [Media API/Media Server](#Media-APIMedia-server)
- [Art Blocks Subgraph](#Art-Blocks-Subgraph-via-The-Graph)

## Hosted APIs

As a quick overview, the main APIs that exist currently are:

<br>

### Token API

Provides the token metadata for a given Art Blocks token.

**Mainnet**

* Note: Contract address is required for Engine

| Contract Type | Pattern | Sample |
| --- | --- | --- |
| Flagship | `https:token.artblocks.io/{tokenID}` | https://token.artblocks.io/0 |
| Engine |  `https:token.artblocks.io/{contractAddress}/{tokenID}` | https://token.artblocks.io/0x0a1bbd57033f57e7b6743621b79fcb9eb2ce3676/110000 |


**Testnet**

| Contract Type | Pattern | Sample |
| --- | --- | --- |
| Flagship | `https:token.staging.artblocks.io/{contractAddress}/{tokenID}` | https://token.staging.artblocks.io/0xda62f67be7194775a75be91cbf9feedcc5776d4b/103000000 |
| Engine | `https:token.staging.artblocks.io/{contractAddress}/{tokenID}` | https://token.staging.artblocks.io/0x81236b5a105d3ad6b56ac41a03e1fd8893a08859/1000001 |

<br>

### Generator API

Provides an i-frame-able live-view for the art associated with a given Art Blocks token.

**Mainnet**

* Note: Contract address is required for Engine

| Contract Type | Pattern | Sample |
| --- | --- | --- |
| Flagship | `https://generator.artblocks.io/{tokenID}` | https://generator.artblocks.io/0 |
| Engine | `https://generator.artblocks.io/{contractAddress}/{tokenID}` | https://generator.artblocks.io/0x0a1bbd57033f57e7b6743621b79fcb9eb2ce3676/11000083 |

**Testnet**

| Contract Type | Pattern | Sample |
| --- | --- | --- |
| Flagship | `https://generator-staging-goerli.artblocks.io/{contractAddress}/{tokenID}` | https://generator-staging-goerli.artblocks.io/0xda62f67be7194775a75be91cbf9feedcc5776d4b/8000002 |
| Engine | `https://generator-staging-goerli.artblocks.io/{contractAddress}/{tokenID}` | https://generator-staging-goerli.artblocks.io/0xe745243b82ebc46e5c23d9b1b968612c65d45f3d/1000001 |

<br>

### Media API/Media server

Provides a static snapshot of the rendered live-view for a given Art Blocks token.

**Mainnet (Flagship)**

| Pattern | Sample |
| --- | --- |
| `https://media.artblocks.io/{tokenID}.png` | https://media.artblocks.io/0.png |

---

In addition to the standard static renders provided for each token, there are two other static renders currently provided: "HD" and "thumbnail". These items can be found at:

* HD Renders – `https://media.artblocks.io/hd/{tokenID}.png`
* Thumbnail Renders – `https://media.artblocks.io/thumb/{tokenID}.png`

Please note that these additional static render formats are still currently being back-filled and may not yet be present for all tokens. Our current recommendation for those looking to depend on the "HD" or "thumbnail" responses is to a) first attempt the HD/thumb image resource that you would pefer, b) if this resource is not available, fall back to the standard sized image resource. For the current state of the ongoing backfill of HD and thumbnail assets, please refer to [this spreadsheet](https://docs.google.com/spreadsheets/d/1Li6TMieXL3MENtg5sq9omRVPsa8MWWb7eZU1uDwYxvU/edit?usp=drive_web&ouid=100711456886886984200).

Please also note that the Generator API and Media API links for a given token are included in the token response for that token from the Token API.

**Mainnet (Engine)**

We are working on a media server for Engine partners. Currently, media is accessible through individual s3 buckets.

| Render Type | Pattern | Sample |
| --- | --- | --- |
| Standard | `https://{enginePartner}-mainnet.s3.amazonaws.com/{tokenID}.png` | https://bright-moments-mainnet.s3.amazonaws.com/8000000.png |
| Thumbnail | `https://{enginePartner}-mainnet.s3.amazonaws.com/thumb/{tokenID}.png` | https://bright-moments-mainnet.s3.amazonaws.com/thumb/8000000.png |

**Testnet**

| Contract Type | Render Type | Pattern | Sample |
| --- | --- | --- | --- |
| Flagship | Standard | `https://art-blocks-artist-staging-goerli.s3.us-west-1.amazonaws.com/{tokenID}.png` | https://art-blocks-artist-staging-goerli.s3.us-west-1.amazonaws.com/10000000.png |
| Engine | Standard | `https://{enginePartner}-goerli.s3.amazonaws.com/{tokenID}.png` | https://bright-moments-goerli.s3.amazonaws.com/1000000.png |


## Art Blocks Subgraph (via The Graph)

The Art Blocks mainnet subgraph on The Graph can currently be queried a few ways:

| The Graph Service | Art Blocks Data | Limited Secondary Sales Data | URL |
| --- | --- | --- | --- |
| Hosted Service | Yes | No | https://thegraph.com/hosted-service/subgraph/artblocks/art-blocks |
| Hosted Service | Yes | Yes^[1] | https://thegraph.com/hosted-service/subgraph/artblocks/art-blocks-with-secondary |
| Decentralized Graph Network | Yes | No | https://thegraph.com/explorer/subgraph?id=0x3c3cab03c83e48e2e773ef5fc86f52ad2b15a5b0-0 |
>[1] Currently limited to OpenSea

<br>

The Art Blocks testnet subgraph on The Graph can be queried at the URL below:

| The Graph Service | Art Blocks Data | URL |
| --- | --- | --- |
| Hosted Service | Yes | https://thegraph.com/hosted-service/subgraph/artblocks/art-blocks-artist-staging-goerli |

**Recommendation:** Using the above links, familiarize yourself with the subgraph’s schema, via the GraphQL playground.

### Subgraph Querying Walkthrough

The following provides some examples on how to use the Art Blocks subgraph to perform a handful of common queries.

#### Important Notes

* Performance/indexing on the hosted subgraph service is oftentimes slower compared to the decentralized subgraph. That being said, the hosted subgraph is free while the decentralized one requires pay-per-query in GRT.
* The Art Blocks subgraphs currently also index any Engine contracts, in addition to the flagship Art Blocks contracts. Please keep that in mind and make use of the `contract_in` filter to ensure you are working with Art Blocks flagship or Engine data, if that is your intention.
* While querying against the mainnet subgraph if using the `contract_in` filter the Art Blocks contracts to restrict for are `0x059edd72cd353df5106d2b9cc5ab83a52287ac3a` (for the V0 contract that supports projects 0-3) and `0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270` (for the V1 contract that supports projects 4-current). 
* The Art Blocks contract to restrict for is `0xda62f67be7194775a75be91cbf9feedcc5776d4b` on testnet.

#### The Basics

Retrieving a specific Art Blocks project by short ID (no contract):

<table>
<tr>
<td> Network </td> <td> Contract Type </td> <td> Query </td>
</tr>
<tr>
<td> Mainnet </td> <td> Flagship </td>
<td>

```graphql
{
  projects(where: {projectId: "0", contract_in: ["0x059edd72cd353df5106d2b9cc5ab83a52287ac3a","0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270"]
  }) {
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
  projects(where: {projectId: "1", contract_in: ["0x0a1bbd57033f57e7b6743621b79fcb9eb2ce3676"]}) {
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
<td> Testnet </td> <td> Flagship </td>
<td>

```graphql
{
  projects(where: {projectId: "100", contract_in: ["0xda62f67be7194775a75be91cbf9feedcc5776d4b"]}) {
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
<td> Testnet </td> <td> Engine </td>
<td>

```graphql
{
  projects(where: {projectId: "1", contract_in: ["0x5503a3b96d845f33f135429ab18c03c79477b14f"]}) {
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

Retrieving a specific Art Blocks project by full ID (includes contract):

<table>
<tr>
<td> Network </td> <td> Contract Type </td> <td> Query </td>
</tr>
<tr>
<td> Mainnet </td> <td> Flagship </td>
<td>

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

</td>
</tr>
<tr>
<td> Mainnet </td> <td> Engine </td>
<td>

```graphql
{
  project(id:"0x0a1bbd57033f57e7b6743621b79fcb9eb2ce3676-1") {
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
<td> Testnet </td> <td> Flagship </td>
<td>

```graphql
{
  project(id:"0xda62f67be7194775a75be91cbf9feedcc5776d4b-100") {
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
<td> Testnet </td> <td> Engine </td>
<td>

```graphql
{
  project(id:"0x5503a3b96d845f33f135429ab18c03c79477b14f-1") {
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
<td> Network </td> <td> Contract Type </td> <td> Query </td>
</tr>
<tr>
<td> Mainnet </td> <td> Flagship </td>
<td>

```graphql
{
  tokens(where: {tokenId: "0", contract_in: ["0x059edd72cd353df5106d2b9cc5ab83a52287ac3a", "0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270"]}) {
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
<tr>
<td> Testnet </td> <td> Flagship </td>
<td>

```graphql
{
  tokens(where: {tokenId: "10000000", contract_in: ["0xda62f67be7194775a75be91cbf9feedcc5776d4b"]}) {
    id
    tokenId
  }
}
```

</td>
</tr>
<tr>
<td> Testnet </td> <td> Engine </td>
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
<td> Network </td> <td> Contract Type </td> <td> Query </td>
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
<tr>
<td> Testnet </td> <td> Flagship </td>
<td>

```graphql
{
  token(id: "0xda62f67be7194775a75be91cbf9feedcc5776d4b-10000000") {
    id
    tokenId
  }
}
```

</td>
</tr>
<tr>
<td> Testnet </td> <td> Engine </td>
<td>

```graphql
{
  token(id: "0x5503a3b96d845f33f135429ab18c03c79477b14f-1000000") {
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

#### Beyond The Basics

Retrieve the last 5 most recently created projects across Art Blocks and Engine (remember that you can use a `contract_in` filter to restrict this to only specific contracts):

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

Retrieve the top 10 projects across Art Blocks Flagship and Engine, based on # of invocations:

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

Retrieve all tokens owned by a specific address, across Art Blocks Flagship and Engine:

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

Retrieve the project script for a given project id

```graphql
{
  project(id:"0x059edd72cd353df5106d2b9cc5ab83a52287ac3a-0") {
    script
  }
}
```

Pagination should be used for large queries. The Graph enforces upper limits on `first` and `skip` parameters since they generally perform poorly when set to large values (limits as of 01/2022 are `first<=1000` and `skip<=5000`). It is much better to page through entities based on an attribute such as token ID, block number, or some other parameter. For more information, see [The Graph documentation](https://thegraph.com/docs/en/developer/graphql-api/#pagination)
