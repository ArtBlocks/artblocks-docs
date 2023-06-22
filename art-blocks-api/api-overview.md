# API Overview

An overview of the current Art Blocks APIs.

Quick Links:
- [Token API](#token-api)
- [Generator API](#generator-api)
- [Media API/Media Server](#media-apimedia-server)
- [Art Blocks Subgraph](#art-blocks-subgraph)
- [GraphQL API](#graphql-api)

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


**Arbitrum One**

* Note: Contract address is required

| Contract Type | Pattern |
| --- | --- |
| Engine |  `https://token.arbitrum.artblocks.io/{contractAddress}/{tokenID}` |

**Arbitrum Testnet**

* Note: Contract address is required

| Contract Type | Pattern |
| --- | --- |
| Engine |  `https://token.arbitrum-staging.artblocks.io/{contractAddress}/{tokenID}` |

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

**Arbitrum One**

* Note: Contract address is required

| Contract Type | Pattern |
| --- | --- |
| Engine |  `https://generator.arbitrum.artblocks.io/{contractAddress}/{tokenID}` |

**Arbitrum Testnet**

* Note: Contract address is required

| Contract Type | Pattern |
| --- | --- |
| Engine |  `https://generator.arbitrum-staging.artblocks.io/{contractAddress}/{tokenID}` |

<br>

### Media API/Media server

Provides a static snapshot of the rendered live-view for a given Art Blocks token.

**Mainnet**

| Contract Type | Pattern | Sample |
| --- | --- | --- |
| Flagship | `https://media.artblocks.io/{tokenID}.png` | https://media.artblocks.io/0.png |
| Engine | `https://media-proxy.artblocks.io/{contractAddress}/{tokenId}.png` | https://media-proxy.artblocks.io/0x145789247973c5d612bf121e9e4eef84b63eb707/782.png |

**Testnet**

| Contract Type | Pattern | Sample |
| --- | --- | --- |
| Flagship | `https://media-proxy-staging.artblocks.io/{tokenID}.png` | https://media-proxy-staging.artblocks.io/0.png |
| Engine | | `https://media-proxy-staging.artblocks.io/{contractAddress}/{tokenID}.png` | https://media-proxy-staging.artblocks.io/0xe745243b82ebc46e5c23d9b1b968612c65d45f3d/1000001 |

**Arbitrum One**

* Note: Contract address is required

| Contract Type | Pattern |
| --- | --- |
| Engine |  `https://media-proxy-arbitrum.artblocks.io/{contractAddress}/{tokenID}` |

**Arbitrum Testnet**

* Note: Contract address is required

| Contract Type | Pattern |
| --- | --- |
| Engine |  `https://media-proxy-arbitrum-staging.artblocks.io/{contractAddress}/{tokenID}` |

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

The Art Blocks Arbitrum subgraphs can be queried at the URLs below:

| The Graph Service | Art Blocks Data | Environment | URL |
| --- | --- | --- | --- |
| Hosted Service | Yes | Production | https://thegraph.com/hosted-service/subgraph/artblocks/art-blocks-arbitrum |
| Hosted Service | Yes | Staging | https://thegraph.com/hosted-service/subgraph/artblocks/art-blocks-staging-arbitrum |

**Recommendation:** Using the above links, familiarize yourself with the subgraph’s schema, via the GraphQL playground.

<br>

### GraphQL API

Provides a broader set of the data that our front-end consumes — this includes both on-chain and off-chain data.

| Chain | Environment | URL |
| --- | --- | --- |
| Ethereum | Production | `https://data.artblocks.io/v1/graphql` |
| Ethereum | Staging | `https://ab-staging-goerli.hasura.app/v1/graphql` |
| Arbitrum | Production | `https://ab-prod-arbitrum.hasura.app/v1/graphql` |
| Arbitrum | Staging | `https://ab-staging-arbitrum.hasura.app/v1/graphql` |

#### Authentication

The following documentation explains how to authenticate with the Art Blocks API to retrieve a JSON Web Token (JWT). This JWT can then be used to gain authenticated access to our GraphQL API. The methods explained here are intended for a client-side environment where a signer is available to sign messages. The procedures are explained using two approaches: Direct API endpoints and GraphQL.

We recommend using the GraphQL-based approach as we have more control over it and can ensure its stability even if underlying API endpoints change. Note that the domain for authentication may change in the future for the Direct API-based approach, while the GraphQL endpoint will remain the same.

##### GraphQL-based Authentication Flow (Recommended)

The GraphQL-based approach leverages the GraphQL schema provided by Art Blocks. This is the recommended approach for stability and future-proofing your implementation.

Here are the functions used in this flow:

```javascript
async function fetchMessageFromApiGql(userAddress) {
  const query = gql`
    query GetAuthMessage($publicAddress: String!, $domain: String!, $uri: String!) {
      getAuthMessage(publicAddress: $publicAddress, domain: $domain, uri: $uri) {
        authMessage
      }
    }
  `;

  const variables = {
    publicAddress: userAddress,
    domain: window.location.host,
    uri: window.location.origin,
  };

  const result = await request(AB_GRAPHQL_ENDPOINT, query, variables);

  if (!result || !result.getAuthMessage) {
    throw new Error("Failed to fetch auth message");
  }

  return result.getAuthMessage.authMessage;
}

async function getJwtGql(userAddress) {
  const message = await fetchMessageFromApiGql(userAddress);

  // Sign message here using the client-side signer
  const signature = /* code to sign message goes here */

  const mutation = gql`
    mutation Authenticate($input: AuthenticateInput!) {
      authenticate(input: $input) {
        jwt
        expiration
      }
    }
  `;

  const variables = {
    input: {
      publicAddress: userAddress,
      message,
      signature
    }
  };

  const result = await request(AB_GRAPHQL_ENDPOINT, mutation, variables);

  if (!result || !result.authenticate) {
    return null;
  }

  return {
    jwt: result.authenticate.jwt,
    expiration: result.authenticate.expiration,
  };
}
```

##### Direct API-based Authentication Flow

The Direct API-based approach involves interacting with the `https://artblocks.io/api/get-auth-message` and `https://artblocks.io/api/authenticate` endpoints. We recommend using the GraphQL-based flow instead because of its improved stability and future-proofing, but we're providing the Direct API-based method for those who prefer it.

> ⚠️ Warning: The domain for authentication may change in the future for the Direct API-based approach. Using the GraphQL-based approach is recommended to avoid future disruptions.

Here are the functions used in this flow:

```javascript
async function fetchMessageFromApi(userAddress) {
  const response = await fetch(AB_MESSAGE_API_URL, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      publicAddress: userAddress,
      domain: window.location.host,
      uri: window.location.origin,
    }),
  });

  const result = await response.json();

  if (!result.ok) {
    throw new Error(result.error);
  }

  return result.data.message;
}

async function getJwtApi(userAddress) {
  const message = await fetchMessageFromApi(userAddress);

  // Sign message here using the client-side signer
  const signature = /* code to sign message goes here */

  const response = await fetch(`${AB_WEBSITE_BASE_URL}/api/authenticate`, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      publicAddress: userAddress,
      signature,
      message
    }),
  });

  const result = await response.json();

  if (!result.ok) {
    return null;
  }

  return result.data.jwt;
}
```

In both methods, you will find a placeholder `/* code to sign message goes here */` where you should implement your code to sign the message using your client-side signer.

##### Using the JWT for Authenticated Access

Once the JWT has been obtained using either of the above methods, it can be used to make authenticated requests to the Art Blocks GraphQL API. The JWT should be included in the `Authorization` header of the request. Here's an example:

```javascript
// Assume jwt contains the JWT you received from the previous steps
const jwt = "your-jwt-token";

// An example of a GraphQL request using the JWT
const query = gql`
  query {
    // Your query here
  }
`;

const response = await fetch(AB_GRAPHQL_ENDPOINT, {
  method: "POST",
  headers: { 
    "Content-Type": "application/json",
    "Authorization": `Bearer ${jwt}`
  },
  body: JSON.stringify({ query }),
});
```

For a full detailed overview of this GraphQL API, please reference: https://docs.artblocks.io/public-api-docs/

Additionally, you can use this interactive Hasura plaground to test out queries: https://cloud.hasura.io/public/graphiql?endpoint=https://data.artblocks.io/v1/graphql
