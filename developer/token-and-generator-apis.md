---
order: 800
description: Art Blocks hosted APIs — token metadata, live generator views, and media proxy.
---

# Token & Generator APIs

Art Blocks hosts three production APIs for integrating with token metadata, live artwork views, and static rendered images. All APIs follow a multichain URL pattern and are available on production and staging (Sepolia testnet) environments.

---

## Supported Networks

| Network      | Chain ID |
| ------------ | -------- |
| Ethereum     | `1`      |
| Arbitrum One | `42161`  |
| Base         | `8453`   |

---

## Token API

Returns the ERC-721 token metadata for a given Art Blocks token, conforming to the OpenSea metadata standard.

**Production**

| Pattern | Example |
| ------- | ------- |
| `https://token.artblocks.io/{chainID}/{contractAddress}/{tokenID}` | [https://token.artblocks.io/1/0x99a9b7c1116f9ceeb1652de04d5969cce509b069/385000000](https://token.artblocks.io/1/0x99a9b7c1116f9ceeb1652de04d5969cce509b069/385000000) |

**Staging (Sepolia testnet)**

| Pattern |
| ------- |
| `https://token.staging.artblocks.io/{chainID}/{contractAddress}/{tokenID}` |

The token metadata response includes the live view URL and media proxy URL for the token, so integrators can retrieve all necessary links from a single API call.

---

## Generator API

Returns an iframe-able live view of the generative artwork associated with a given token. The live view runs the artist's script in the browser using the token's hash.

**Production**

| Pattern | Example |
| ------- | ------- |
| `https://generator.artblocks.io/{chainID}/{contractAddress}/{tokenID}` | [https://generator.artblocks.io/1/0x99a9b7c1116f9ceeb1652de04d5969cce509b069/385000000](https://generator.artblocks.io/1/0x99a9b7c1116f9ceeb1652de04d5969cce509b069/385000000) |

**Staging (Sepolia testnet)**

| Pattern |
| ------- |
| `https://generator.staging.artblocks.io/{chainID}/{contractAddress}/{tokenID}` |

The generator URL is also included in the token metadata response from the Token API.

---

## Media Proxy API

Returns a static rendered image (PNG) of the token's artwork, captured by a headless browser. This is the canonical static image used on Art Blocks and marketplaces.

**Production**

| Pattern | Example |
| ------- | ------- |
| `https://media-proxy.artblocks.io/{chainID}/{contractAddress}/{tokenID}.png` | [https://media-proxy.artblocks.io/1/0x99a9b7c1116f9ceeb1652de04d5969cce509b069/385000000.png](https://media-proxy.artblocks.io/1/0x99a9b7c1116f9ceeb1652de04d5969cce509b069/385000000.png) |

**Staging (Sepolia testnet)**

| Pattern |
| ------- |
| `https://media-proxy.staging.artblocks.io/{chainID}/{contractAddress}/{tokenID}.png` |

---

## Art Blocks Subgraph

Art Blocks maintains subgraphs on [The Graph Network](https://thegraph.com/) for each supported production network. Subgraphs provide efficient access to on-chain data (token ownership, project metadata, minting history) without querying the blockchain directly.

The subgraph source code is developed publicly at [github.com/ArtBlocks/artblocks-subgraph](https://github.com/ArtBlocks/artblocks-subgraph).

### Endpoints

**Ethereum Mainnet**

- [Explorer Page](https://thegraph.com/explorer/subgraphs/6bR1oVsRUUs6czNiB6W7NNenTXtVfNd5iSiwvS4QbRPB?view=Overview&chain=arbitrum-one)
- GraphQL: `https://gateway-arbitrum.network.thegraph.com/api/[api-key]/subgraphs/id/6bR1oVsRUUs6czNiB6W7NNenTXtVfNd5iSiwvS4QbRPB`

**Arbitrum One**

- [Explorer Page](https://thegraph.com/explorer/subgraphs/5WwGsBwJ2hVBpc3DphX4VHVMsoPnRkVkuZF4HTArZjCm?view=Overview&chain=arbitrum-one)
- GraphQL: `https://gateway-arbitrum.network.thegraph.com/api/[api-key]/subgraphs/id/5WwGsBwJ2hVBpc3DphX4VHVMsoPnRkVkuZF4HTArZjCm`

**Base**

- [Explorer Page](https://thegraph.com/explorer/subgraphs/5gKxDMnBjv3ffBJ4r3zWD6VrpaYHiq9aUth39YCQXWEt?view=Overview&chain=arbitrum-one)
- GraphQL: `https://gateway-arbitrum.network.thegraph.com/api/[api-key]/subgraphs/id/5gKxDMnBjv3ffBJ4r3zWD6VrpaYHiq9aUth39YCQXWEt`

### Helpful Resources

- [Video tutorial: Creating an API Key](https://www.youtube.com/watch?v=UrfIpm-Vlgs)
- [Managing your API Key](https://thegraph.com/docs/en/studio/managing-api-keys/)
- [Querying from an application](https://thegraph.com/docs/en/developer/querying-from-your-app/)

---

## GraphQL API (Hasura)

For most integrations, the Art Blocks GraphQL API (Hasura) is the recommended data source. It provides both on-chain and off-chain data — including minter configuration details, media URLs, project descriptions, and more — that are not available from the subgraph alone.

| Environment               | URL                                                |
| ------------------------- | -------------------------------------------------- |
| Production                | `https://data.artblocks.io/v1/graphql`             |
| Staging (Sepolia testnet) | `https://ab-staging-sepolia.hasura.app/v1/graphql` |

The API uses `_metadata` table suffixes (e.g. `projects_metadata`, `tokens_metadata`) and supports filtering by `chain_id`. An interactive playground is available at:

[https://cloud.hasura.io/public/graphiql?endpoint=https://data.artblocks.io/v1/graphql](https://cloud.hasura.io/public/graphiql?endpoint=https://data.artblocks.io/v1/graphql)

For full schema reference and example queries, see the [GraphQL Reference](/developer/graphql/).

For AI-assisted GraphQL querying, the [Art Blocks MCP Server](/developer/mcp-server/quick-start/) provides `explore_table`, `build_query`, and `graphql_query` tools that handle field validation, chain filtering, and query construction automatically.
