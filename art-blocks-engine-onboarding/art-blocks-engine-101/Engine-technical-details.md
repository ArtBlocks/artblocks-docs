# Art Blocks Engine Flex Technical Details

This page goes deeper into some technical considerations when working with the most current version of Artblocks Engine Flex.
The latest version of the Engine Flex contract (v3) and interface can be found here:
- https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/contracts/engine/V3/GenArt721CoreV3_Engine_Flex.sol
- https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/contracts/interfaces/0.8.x/IGenArt721CoreContractV3_Engine_Flex.sol

## Introduction To External Asset Dependencies

```solidity
struct ExternalAssetDependency {
        string cid;
        ExternalAssetDependencyType dependencyType;
        address bytecodeAddress;
}
```

The Engine Flex contract introduces the concept of external asset dependencies. These essentially function as on-chain pointers to off-chain assets stored using decentralized storage technologies and, with the latest version of flex, also supports fully on-chain data storage. An external asset dependency is comprised of its content identifier (CID), if it's using Arweave or IPFS, a bytecodeAddress if it's specifically dealing with fully on-chain data, and a dependencyType, which maps to an Engine Flex supported platform.

Engine Flex currently supports adding external asset dependencies of the following types:
- IPFS
- Arweave
- Onchain (data lives entirely on the blockchain)

## Adding, Updating & Removing External Asset Dependencies

When working with and manipulating a project's external asset dependencies, you'll be relying on the following functions:

```solidity
function addProjectExternalAssetDependency(uint256 _projectId, string memory _cidOrData, ExternalAssetDependencyType _dependencyType)
function updateProjectExternalAssetDependency(uint256 _projectId, uint256 _index, string memory _cidOrData, ExternalAssetDependencyType _dependencyType)
function removeProjectExternalAssetDependency(uint256 _projectId, uint256 _index)
```
Note the parameter `_cidOrData`, which allows you to either pass in a CID if you are working with the IPFS/Arweave dependencyTypes or a data string if you are working with the onchain dependencyType.

For convenience and utility, the contract also provides the following function, allowing you to easily grab a project's external asset dependency at a specific index:
```solidity
function projectExternalAssetDependencyByIndex(uint256 _projectId, uint256 _index)
```
This convenience function returns data in the form of the following format:
```solidity
/**
* @notice An external asset dependency with data. This is a convenience struct that contains the CID of the dependency,
* the type of the dependency, the address of the bytecode for this dependency, and the data retrieved from this bytecode address.
*/
struct ExternalAssetDependencyWithData {
        string cid;
        ExternalAssetDependencyType dependencyType;
        address bytecodeAddress;
        string data;
}
```
Note that for dependencyTypes other than onchain (IPFS, Arweave), the returned bytecodeAddress will be the zero address and data will be an empty string. Conversely, if the dependencyType is onchain, the returned cid will be an empty string.

Some important factors to keep in mind with the above functions:
- Only allowlisted/artist addresses can call these.
- `ExternalAssetDependencyType _dependencyType` is a solidity enum, which can be passed into these functions as a uint8. This enum only defines three options as of now, `IPFS`,`ARWEAVE`, and `ONCHAIN`, which can be represented as `0`,`1`, and `2` respectively.

### Note On Removing External Asset Dependencies

In the interest of saving gas, the `removeProjectExternalAssetDependency()` function is implemented in such a way that it does not preserve the order of the project's external asset dependency mapping. Specifically, the way this removal logic works is as follows: when an index to remove is passed in, the element at that index being removed is swapped with the element at the last index of the list of assets. Now that the last index holds the element to be removed, that element is removed off the list. This method, in addition to being more gas efficient, also ensures that our list/mapping does not have any "holes". The tradeoff, however, is that the removal causes the order of the external asset dependencies in this list to change, albeit in a deterministic manner: the element at the last index always moves to the removed index. This is important to keep in mind when writing your project script, though you can always update the ordering manually as you see fit by utilizing the `updateProjectExternalAssetDependency()` function.

You can view directly the full implementation of this removal function here: https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/contracts/engine/V3/GenArt721CoreV3_Engine_Flex.sol#L524

## Preferred Gateways

```solidity
string public preferredIPFSGateway;
string public preferredArweaveGateway;
```

The Engine Flex contract allows you to specify preferred gateways for the currently supported dependency types (IPFS & Arweave). Gateways are accessible HTTP interfaces and, when combined with an asset CID, expose urls for assets being stored on these off-chain decentralized platforms. These preferred gateways are updateable with a string param via the following functions: `updateArweaveGateway()` & `updateIPFSGateway()`.

Please note that these preferred gateways are set per-contract, not per-project.

## Working With External Asset Dependencies In Your Project Script

When you request the live view for a given token of a project, the `hash` and `tokenId` of the token are provided in the `tokenData` object and the Art Blocks Generator injects this into the served HTML live view. This `tokenData` object has now been extended with the following external asset dependency related data, if it is available:

```js
let tokenData = {
  hash: "",
  tokenId:"",
  externalAssetDependencies: [
    {
      cid: "",
      dependencyType: "",
      data: ""
    },
    ...
  ],
  preferredIPFSGateway:"",
  preferredArweaveGateway: ""
}
```

Your project script can then easily make use of these dependencies by combining the CID of the asset with the appropriate gateway, if you are dealing with IPFS/Arweave dependencies. As a simple example: If you have an external asset dependency with a CID `QmXxgX5Qyhqz1t9wDFkvJtjVKYe1f8Uj714RV2n1LS76Pg` and a dependencyType of `IPFS`, you can construct the full url of your external asset dependency by combining the `preferredIPFSGateway`, which let's assume is `https://ipfs.io/ipfs/`, with the asset CID. This gives you the full url of the asset, `https://ipfs.io/ipfs/QmXxgX5Qyhqz1t9wDFkvJtjVKYe1f8Uj714RV2n1LS76Pg`, and allows your project script to download it with `fetch` and use it as it sees fit. For fully onchain external asset dependencies, the full data string that is stored on the blockchain will be injected.

Note that for IPFS/Arweave external asset dependencies if your CID is pointing to a directory of assets, rather than a single asset, your project script will need to be aware of the file naming structure of this directory to fetch the assets individually. Using the previous example, imagine that CID `QmXxgX5Qyhqz1t9wDFkvJtjVKYe1f8Uj714RV2n1LS76Pg` was pointing to a directory of 10 PNG images, with filenames corresponding to the numbers 1-10. Your project script would generate the same full url with the information provided, `https://ipfs.io/ipfs/QmXxgX5Qyhqz1t9wDFkvJtjVKYe1f8Uj714RV2n1LS76Pg`, but also append the specific file you want to fetch by being aware of the naming conventions, ie `https://ipfs.io/ipfs/QmXxgX5Qyhqz1t9wDFkvJtjVKYe1f8Uj714RV2n1LS76Pg/1.png`.

## Loading JS Libraries As External Asset Dependencies

If you are specifically looking to utilize an IPFS/ARWEAVE type external asset dependency as a JavaScript library in your project script, you cannot simply add it as a script element onto the page. You must load it in a blocking manner so that the browser does not attempt to run your project script code before the lib is  fully loaded. Here is an example of how to do this with ES6 dynamic imports (supported by most modern browsers: https://caniuse.com/es6-module-dynamic-import):

```js
(async () => {
        await import('JS_EXTERNAL_ASSET_DEPENDENCY_FULL_URL_GOES_HERE');

        // project script follows below
})()
```

Here's another method without using ES6 dynamic imports, instead relying on using a callback that gets fired after the JS external asset dependency is injected into the html via a script tag:
```js
function loadScript(url, callback)
{
    // adding the script element to the head
   var head = document.getElementsByTagName('head')[0];
   var script = document.createElement('script');
   script.type = 'text/javascript';
   script.src = url;

   // then bind the event to the callback function
   // there are several events for cross browser compatibility
   script.onreadystatechange = callback;
   script.onload = callback;

   // fire the loading
   head.appendChild(script);
}

const myProjectScriptCode = function() { .... }

loadScript('JS_EXTERNAL_ASSET_DEPENDENCY_FULL_URL_GOES_HERE', myProjectScriptCode);
```

## Locking A Project's External Asset Dependencies

Artists and allowlisted addresses also have the ability to lock a project's external asset dependencies:
```solidity
function lockProjectExternalAssetDependencies(uint256 _projectId)
```
This irreversible action removes the ability to add, update or remove from a project's external asset dependencies.

Important notes:
- Preferred gateways do not get locked with this action and, in general, cannot be locked. This is intentional to allow support for modifying the preferred gateway over time, which may change while CIDs remain fixed/permanent.
- You can lock a project's external asset dependencies regardless of whether or not the project itself is locked. And you can continue to modify a project's external dependencies even if the project is locked, as long as the external asset dependencies for the project are not locked.

## Why should I use the Engine Flex specific fields for CIDs and IPFS gateways rather than hard-coding these values in the script?

The Engine Flex contract was designed to expose specific on-contract fields for storing external asset dependencies (either via auxiliary on-chain storage, IPFS CIDs, or Arweave CIDs). For collectors and archivists preserving these art works, this increases the introspect-ability of where these external assets are stored, e.g. allowing for a more streamlined and robust process for replicating external assets stored on IPFS for a given project in the future.

Additionally, after project scripts are locked, if an IPFS gateway is hardcoded it isn't possible to update this in the future if the gateway (but not the underlying asset CIDs) needs to change for whatever reason (partner is migrating gateway providers from Pinata to Infura, partner is shutting down private gateway in favor of a public one, etc.). If using the specified on-chain fields, the CIDs can be locked independently from the gateway, allowing flexibility to preserve future compatibility of the on-chain generator down the road.
