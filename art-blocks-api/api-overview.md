# API Overview

An overview of the current Art Blocks APIs.

Quick Links:

- [Token API](#token-api)
- [Generator API](#generator-api)
- [Media Proxy API](#media-proxy-api)
- [Art Blocks Subgraph](#art-blocks-subgraph)
- [GraphQL API](#graphql-api)

## Supported Networks

Art Blocks is currently deployed on the following networks:

| Network      | Chain ID |
| ------------ | -------- |
| Ethereum     | `1`      |
| Arbitrum One | `42161`  |
| Base         | `8453`   |

All hosted APIs below follow a **multichain URL pattern** using the chain ID to specify the target network.

## Hosted APIs

<br>

### Token API

Provides the token metadata for a given Art Blocks token.

**Production**

| Pattern                                                            | Example                                                                           |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------- |
| `https://token.artblocks.io/{chainID}/{contractAddress}/{tokenID}` | https://token.artblocks.io/1/0x99a9b7c1116f9ceeb1652de04d5969cce509b069/385000000 |

**Staging**

| Pattern                                                                    |
| -------------------------------------------------------------------------- |
| `https://token.staging.artblocks.io/{chainID}/{contractAddress}/{tokenID}` |

**Dev**

| Pattern                                                                |
| ---------------------------------------------------------------------- |
| `https://token.dev.artblocks.io/{chainID}/{contractAddress}/{tokenID}` |

<br>

### Generator API

Provides an i-frame-able live-view for the art associated with a given Art Blocks token.

**Production**

| Pattern                                                                | Example                                                                               |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| `https://generator.artblocks.io/{chainID}/{contractAddress}/{tokenID}` | https://generator.artblocks.io/1/0x99a9b7c1116f9ceeb1652de04d5969cce509b069/385000000 |

**Staging**

| Pattern                                                                        |
| ------------------------------------------------------------------------------ |
| `https://generator.staging.artblocks.io/{chainID}/{contractAddress}/{tokenID}` |

**Dev**

| Pattern                                                                    |
| -------------------------------------------------------------------------- |
| `https://generator.dev.artblocks.io/{chainID}/{contractAddress}/{tokenID}` |

<br>

### Media Proxy API

Provides a static snapshot of the rendered live-view for a given Art Blocks token.

**Production**

| Pattern                                                                      | Example                                                                                     |
| ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `https://media-proxy.artblocks.io/{chainID}/{contractAddress}/{tokenID}.png` | https://media-proxy.artblocks.io/1/0x99a9b7c1116f9ceeb1652de04d5969cce509b069/385000000.png |

**Staging**

| Pattern                                                                              |
| ------------------------------------------------------------------------------------ |
| `https://media-proxy.staging.artblocks.io/{chainID}/{contractAddress}/{tokenID}.png` |

**Dev**

| Pattern                                                                          |
| -------------------------------------------------------------------------------- |
| `https://media-proxy.dev.artblocks.io/{chainID}/{contractAddress}/{tokenID}.png` |

Please note that the Generator API and Media Proxy API links for a given token are included in the token response for that token from the Token API.

---

## Art Blocks Subgraph

Art Blocks has subgraphs deployed to [The Graph Network](https://thegraph.com/docs/en/network/overview/) for every supported production network.

These subgraphs can be used to query for on-chain data related to the Art Blocks contracts, including token data and project data. They provide a way to access on-chain data in a more efficient and user-friendly way than directly querying the blockchain, while keeping infrastructure decentralized, transparent, and reliable.

The Art Blocks subgraph is developed in public, and all source code and development activity can be found in the [Art Blocks subgraph repository](https://github.com/ArtBlocks/artblocks-subgraph).

### Ethereum Mainnet

- [Explorer Page](https://thegraph.com/explorer/subgraphs/6bR1oVsRUUs6czNiB6W7NNenTXtVfNd5iSiwvS4QbRPB?view=Overview&chain=arbitrum-one)
- Graphql Endpoint: `https://gateway-arbitrum.network.thegraph.com/api/[api-key]/subgraphs/id/6bR1oVsRUUs6czNiB6W7NNenTXtVfNd5iSiwvS4QbRPB`

### Arbitrum One

- [Explorer Page](https://thegraph.com/explorer/subgraphs/5WwGsBwJ2hVBpc3DphX4VHVMsoPnRkVkuZF4HTArZjCm?view=Overview&chain=arbitrum-one)
- Graphql Endpoint: `https://gateway-arbitrum.network.thegraph.com/api/[api-key]/subgraphs/id/5WwGsBwJ2hVBpc3DphX4VHVMsoPnRkVkuZF4HTArZjCm`

### Base

- [Explorer Page](https://thegraph.com/explorer/subgraphs/5gKxDMnBjv3ffBJ4r3zWD6VrpaYHiq9aUth39YCQXWEt?view=Overview&chain=arbitrum-one)
- Graphql Endpoint: `https://gateway-arbitrum.network.thegraph.com/api/[api-key]/subgraphs/id/QmNMohwC881f9KTiVWtQx2eQ5pNSsnMaSYQqwypX9x5fFZ`

### Helpful Resources

- [Video Tutorial on creating an API Key](https://www.youtube.com/watch?v=UrfIpm-Vlgs)
- [Managing your API Key & setting your indexer preferences](https://thegraph.com/docs/en/studio/managing-api-keys/)
- [Querying from an application](https://thegraph.com/docs/en/developer/querying-from-your-app/)
- [How to use the explorer and playground to query on-chain data](https://medium.com/@chidubem_/how-to-query-on-chain-data-with-the-graph-f8507488215)

## Querying the Subgraph

The Art Blocks subgraphs can be queried at any of the graphql endpoints listed in the previous section. For richer context — including off-chain data and minter configuration details — we recommend using the [Art Blocks GraphQL API](#graphql-api).

## GraphQL API

Provides a broader set of data than the subgraph alone — this includes both on-chain and off-chain data. We recommend using this API for most integrations, as it provides a more complete picture of projects, tokens, and minting configurations.

| Environment | URL                                                |
| ----------- | -------------------------------------------------- |
| Production  | `https://data.artblocks.io/v1/graphql`             |
| Staging     | `https://ab-staging-sepolia.hasura.app/v1/graphql` |

The GraphQL API uses `_metadata` table suffixes (e.g. `projects_metadata`, `tokens_metadata`, `contracts_metadata`, `minters_metadata`) and provides fields such as `chain_id`, `contract_address`, minter configuration details, and more. See the [Entities](/creator-docs/art-blocks-api/entities/) page for a full reference.

For a full detailed overview of this GraphQL API, please reference: https://docs.artblocks.io/public-api-docs/

Additionally, you can use this interactive Hasura playground to test out queries: https://cloud.hasura.io/public/graphiql?endpoint=https://data.artblocks.io/v1/graphql
