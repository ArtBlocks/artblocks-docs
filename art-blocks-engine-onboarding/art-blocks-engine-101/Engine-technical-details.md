# Art Blocks Engine Flex Technical Details

This page goes deeper into some technical considerations when working with Artblocks Engine Flex

## Introduction To External Asset Dependencies

```solidity
struct ExternalAssetDependency {
        string cid;
        ExternalAssetDependencyType dependencyType;
}
```

The Engine Flex contract introduces the concept of external asset dependencies. These essentially function as on-chain pointers to off-chain, decentralized assets stored on supported platforms. An external asset dependency is comprised of its content indentifier (CID) and dependencyType, which maps to an Engine Flex supported platform. Engine Flex currently supports adding external asset dependencies from the following platforms:
- IPFS
- Arweave

## Preferred Gateways

```solidity
string public preferredIPFSGateway;
string public preferredArweaveGateway;
```

The Engine Flex contract allows you to specify preferred gateways for the currently supported dependency types (IPFS & Arweave). These are updateable with a string param via the following functions: `updateArweaveGateway()` & `updateIPFSGateway()` Please note that these preferred gateways are set per-contract, not per-project.

## Working With Exeternal Asset Dependencies In Your Project Script

When you request the live view for a given token of a project, the `hash` and `tokenId` of the token are provided in the `tokenData` object and the Art Blocks Generator inject this into the served HTML live view. This `tokenData` object has now been extended with the following external asset dependency related data if it is available:

```js
let tokenData = {
  hash: "",
  tokenId:"",
  externalAssetDependencies: [
    {
      cid: "",
      dependencyType: ""
    },
    ...
  ],
  preferredIPFSGateway:"",
  preferredArweaveGateway: ""
}
```

Your project script can then easily make use of these dependencies by combining the CID of the asset with the appropriate gateway. As a simple example: If you have an external asset dependency with a CID `QmXxgX5Qyhqz1t9wDFkvJtjVKYe1f8Uj714RV2n1LS76Pg` and a dependencyType of `IPFS`, you can construct the full url of your external asset depdency by combining the `preferredIPFSGateway`, which let's assume is `https://ipfs.io/ipfs/`, with the asset CID. This gives you the full url of the asset, `https://ipfs.io/ipfs/QmXxgX5Qyhqz1t9wDFkvJtjVKYe1f8Uj714RV2n1LS76Pg`, and allows your project script to download it with `fetch` and use it as it sees fit.

## Loading JS Libraries As External Asset Dependencies

[TBD]
