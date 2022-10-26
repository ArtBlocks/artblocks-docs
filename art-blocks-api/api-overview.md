# API Overview

An overview of the current Art Blocks APIs.

!!!
We are currently in the process of working on finalizing a more comprehensive project-oriented API which we plan to release in the first half of 2022. This API will encapsulate both onchain data (the information readily available via the Art Blocks public subgraph on The Graph) and additional off-chain data (e.g., all available features for a given project)
!!!

Quick Links:
- [Token API](#token-api)
- [Generator API](#generator-api)
- [Media API/Media Server](#media-apimedia-server)
- [Art Blocks Subgraph](#art-blocks-subgraph)

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



## Art Blocks Subgraph

Art Blocks has a GraphQL API Endpoint hosted by [The Graph](https://thegraph.com/docs/about/introduction#what-the-graph-is) called a subgraph for indexing and organizing data from the Art Blocks smart contracts.

This subgraph can be used to query for on-chain data related to the Art Blocks contracts.

Subgraph information is serviced by a decentralized group of server operators called Indexers.

## Ethereum Mainnet

- [Explorer Page](https://thegraph.com/explorer/subgraph?id=5So3nipgHT3ks7pEPDQ6YgSFhfEmADrh481P9z1ZtcMA&view=Overview)
- Graphql Endpoint: https://api.thegraph.com/subgraphs/name/yyd01245/artblocks
- [Code Repo](https://github.com/ArtBlocks/artblocks-subgraph)

## Helpful Resources

<br>
- [Video Tutorial on creating an API Key](https://www.youtube.com/watch?v=UrfIpm-Vlgs)
- [Managing your API Key & setting your indexer preferences](https://thegraph.com/docs/en/studio/managing-api-keys/)
- [Querying from an application](https://thegraph.com/docs/en/developer/querying-from-your-app/)
- [How to use the explorer and playground to query on-chain data](https://medium.com/@chidubem_/how-to-query-on-chain-data-with-the-graph-f8507488215)


## The Art Blocks mainnet subgraph can currently be queried a few ways:

| The Graph Service           | Art Blocks Data | Limited Secondary Sales Data | URL                                                                                    |
| --------------------------- | --------------- | ---------------------------- | -------------------------------------------------------------------------------------- |
| Hosted Service              | Yes             | No                           | https://thegraph.com/hosted-service/subgraph/artblocks/art-blocks                      |
| Hosted Service              | Yes             | Yes^[1]                      | https://thegraph.com/hosted-service/subgraph/artblocks/art-blocks-with-secondary       |
| Decentralized Graph Network | Yes             | No                           | https://thegraph.com/explorer/subgraph?id=0x3c3cab03c83e48e2e773ef5fc86f52ad2b15a5b0-0 |

> [1] Currently limited to OpenSea & LooksRare

<br>

The Art Blocks testnet subgraph can be queried at the URL below:

| The Graph Service | Art Blocks Data | URL |
| --- | --- | --- |
| Hosted Service | Yes | https://thegraph.com/hosted-service/subgraph/artblocks/art-blocks-artist-staging-goerli |

**Recommendation:** Using the above links, familiarize yourself with the subgraph’s schema, via the GraphQL playground.
