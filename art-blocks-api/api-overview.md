# Artblock Subgraph Introduction

Artblocks has a GraphQL API Endpoint hosted by [The Graph](https://thegraph.com/docs/about/introduction#what-the-graph-is) called a subgraph for indexing and organizing data from the Artblocks smart contracts.

This subgraph is can be used to query Artblock data.

Subgraph information is serviced by a decentralized group of server operators called Indexers.

## Ethereum Mainnet

- [Explorer Page](https://thegraph.com/explorer/subgraph?id=5So3nipgHT3ks7pEPDQ6YgSFhfEmADrh481P9z1ZtcMA&view=Overview)
- Graphql Endpoint: https://api.thegraph.com/subgraphs/name/yyd01245/artblocks
- [Code Repo](https://github.com/ArtBlocks/artblocks-subgraph)

## Helpful Resources

- [Video Tutorial on creating an API Key](https://www.youtube.com/watch?v=UrfIpm-Vlgs)
- [Managing your API Key & setting your indexer preferences](https://thegraph.com/docs/en/studio/managing-api-keys/)
- [Querying from an application](https://thegraph.com/docs/en/developer/querying-from-your-app/)
- [How to use the explorer and playground to query on-chain data](https://medium.com/@chidubem_/how-to-query-on-chain-data-with-the-graph-f8507488215)

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

- HD Renders – `https://media.artblocks.io/hd/{tokenID}.png`
- Thumbnail Renders – `https://media.artblocks.io/thumb/{tokenID}.png`

!!!
Please note that these additional static render formats are still currently being back-filled and may not yet be present for all tokens. Our current recommendation for those looking to depend on the "HD" or "thumbnail" responses is to a) first attempt the HD/thumb image resource that you would pefer, b) if this resource is not available, fall back to the standard sized image resource.
!!!

For the current state of the ongoing backfill of HD and thumbnail assets, please refer to [this spreadsheet](https://docs.google.com/spreadsheets/d/1Li6TMieXL3MENtg5sq9omRVPsa8MWWb7eZU1uDwYxvU/edit?usp=drive_web&ouid=100711456886886984200)

Please also note that the Generator API and Media API links for a given token are included in the token response for that token from the Token API.

## The Art Blocks mainnet subgraph on The Graph can currently be queried a few ways:

| The Graph Service           | Art Blocks Data | Limited Secondary Sales Data | URL                                                                                    |
| --------------------------- | --------------- | ---------------------------- | -------------------------------------------------------------------------------------- |
| Hosted Service              | Yes             | No                           | https://thegraph.com/hosted-service/subgraph/artblocks/art-blocks                      |
| Hosted Service              | Yes             | Yes^[1]                      | https://thegraph.com/hosted-service/subgraph/artblocks/art-blocks-with-secondary       |
| Decentralized Graph Network | Yes             | No                           | https://thegraph.com/explorer/subgraph?id=0x3c3cab03c83e48e2e773ef5fc86f52ad2b15a5b0-0 |

> [1] Currently limited to OpenSea

**Recommandation:** Using the above links, familiarize yourself with the subgraph’s schema, via the GraphQL playground.