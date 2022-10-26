---
sidebar_position: 3
title: Querying and API Overview

---

# Querying

Below are some sample queries you can use to gather information from the Art Blocks contracts.

You can build your own queries using a [GraphQL Explorer](https://graphiql-online.com/graphiql) and enter your endpoint to limit the data to exactly what you need.

## Subgraph Querying Walkthrough

The following provides some examples on how to use the Art Blocks subgraph to perform a handful of common queries.

#### Important Notes

- Performance/indexing on the hosted subgraph service is oftentimes slower compared to the decentralized subgraph. That being said, the hosted subgraph is free while the decentralized one requires pay-per-query in GRT.
- The Art Blocks subgraphs currently also index any PBAB (Powered by Artblocks) contracts, in addition to the core Art Blocks contracts. Please keep that in mind and make use of the `contract_in` filter to ensure you are working with Art Blocks data only, if that is your intention.
* While querying against the mainnet subgraph if using the `contract_in` filter the Art Blocks contracts to restrict for are `0x059edd72cd353df5106d2b9cc5ab83a52287ac3a` (for the V0 contract that supports projects 0-3) and `0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270` (for the V1 contract that supports projects 4-current). 
* The Art Blocks contract to restrict for is `0xda62f67be7194775a75be91cbf9feedcc5776d4b` on testnet.

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
<td> Network </td> <td> Contract Type </td> <td style="width:700px"> Query </td>
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

- Pull all projects and return their name, as well as lots of additional data:

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

- Get all the wallet owners of a project (Replace PROJECT with the project name you are looking for)

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

- Get that txnhash for squiggle 0, you could run the following query on the AB subgraph playground

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
