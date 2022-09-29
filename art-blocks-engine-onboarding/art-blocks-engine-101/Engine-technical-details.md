# Art Blocks Engine Flex Technical Details

This page goes deeper into some technical considerations when working with Artblocks Engine Flex

## Introduction To External Asset Dependencies

```solidity
struct ExternalAssetDependency {
        string cid;
        ExternalAssetDependencyType dependencyType;
}
```

The Engine Flex contract introduces the concept of external asset dependencies. These essentially function as on-chain pointers to off-chain assets stored using decentralized storage technologies. An external asset dependency is comprised of its content indentifier (CID) and dependencyType, which maps to an Engine Flex supported platform. 

Engine Flex currently supports adding external asset dependencies hosted using the following decentralized storage solutions:
- IPFS
- Arweave

## Adding, Updating & Removing External Asset Dependencies

When working with and manipulating a project's external asset dependencies, you'll be relying on the following functions:

```solidity
function addProjectExternalAssetDependency(uint256 _projectId, string calldata _cid, ExternalAssetDependencyType _dependencyType)
function updateProjectExternalAssetDependency(uint256 _projectId, uint256 _index, string calldata _cid, ExternalAssetDependencyType _dependencyType)
function removeProjectExternalAssetDependency(uint256 _projectId, uint256 _index)
```

For convenience and utility, the contract also provides the following function, allowing you to easily grab a project's external asset dependency at a specific index:
```solidity
function projectExternalAssetDependencyByIndex(uint256 _projectId, uint256 _index) 
```

Some important factors to keep in mind with the above functions:
- Only allowlisted/artist addresses can call these.
- `ExternalAssetDependencyType _dependencyType` is a solidity enum, which can be passed in to these functions as a uint8. This enum only defines two options as of now, `IPFS` and `ARWEAVE`, which can be represented as `0` and `1` respectively. 

### Note On Removing External Asset Dependencies
 
In the interest of saving gas, the `removeProjectExternalAssetDependency()` function is implemented in such a way that it does not preserve the order of the project's external asset dependency mapping. Specifically, the way this removal logic works is as follows: when an index to remove is passed in, the element at that index being removed is swapped with the element at the last index of the list of assets. Now that the last index holds the element to be removed, that element is removed off the list. This method, in addition to being more gas efficient, also ensures that our list/mapping does not have any "holes''. The tradeoff, however, is that the removal causes the order of the external asset dependencies in this list to change, albeit in a deterministic manner: the element at the last index always moves to the removed index. This is important to keep in mind when writing your project script, though you can always update the ordering manually as you see fit by utilizing the `updateProjectExternalAssetDependency()` function.

You can view directly the full implementation of this removal function here: https://github.com/ArtBlocks/artblocks-contracts/blob/main/contracts/PBAB%2BCollabs/GenArt721CoreV2_ENGINE_FLEX.sol#L596

## Preferred Gateways

```solidity
string public preferredIPFSGateway;
string public preferredArweaveGateway;
```

The Engine Flex contract allows you to specify preferred gateways for the currently supported dependency types (IPFS & Arweave). Gateways are accessible HTTP interfaces and, when combined with an asset CID, expose urls for assets being stored on these off-chain decentralized platforms. These preferred gateways are updateable with a string param via the following functions: `updateArweaveGateway()` & `updateIPFSGateway()`.       

Please note that these preferred gateways are set per-contract, not per-project.

## Working With Exeternal Asset Dependencies In Your Project Script

When you request the live view for a given token of a project, the `hash` and `tokenId` of the token are provided in the `tokenData` object and the Art Blocks Generator injects this into the served HTML live view. This `tokenData` object has now been extended with the following external asset dependency related data, if it is available:

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

Note that if your CID is pointing to a directory of assets, rather than a single asset, your project script will need to be aware of the file naming structure of this directory to fetch the assets individually. Using the previous example, imagine that CID `QmXxgX5Qyhqz1t9wDFkvJtjVKYe1f8Uj714RV2n1LS76Pg` was pointing to a directory of 10 PNG images, with filenames corresponding to the numbers 1-10. Your project script would generate the same full url with the information provided, `https://ipfs.io/ipfs/QmXxgX5Qyhqz1t9wDFkvJtjVKYe1f8Uj714RV2n1LS76Pg`, but also append the specific file you want to fetch by being aware of the naming conventions, ie `https://ipfs.io/ipfs/QmXxgX5Qyhqz1t9wDFkvJtjVKYe1f8Uj714RV2n1LS76Pg/1.png`.

## Loading JS Libraries As External Asset Dependencies

If you are specifically looking to utilize an external asset dependency as a JavaScript library in your project script, you cannot simply add it as a script element onto the page. You must load it in a blocking manner so that the browser does not attempt to run your project script code before the lib is  fully loaded. Here is an example of how to do this with ES6 dynamic imports (supported by most modern browsers: https://caniuse.com/es6-module-dynamic-import):

```js
(async () => {
        await import('JS_EXTERNAL_ASSET_DEPENDENCY_FULL_URL_GOES_HERE');
    
        // project script follows bellow
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

Artists and allowlisted addresses also have the ability to lock a project's external asset depdencies:
```solidity
function lockProjectExternalAssetDependencies(uint256 _projectId)
```
This irreversible action removes the ability to add, update or remove from a project's external asset dependencies.

Important notes:
- Preferrred gateways do not get locked with this action and, in general, cannot be locked. This is intentional to allow support for modifying the preferred gateway over time, which may change while CIDs remain fixed/permanent.
- You can lock a project's external asset dependencies regardless of whether or not the project itself is locked. And you can continue to modify a project's external dependencies even if the project is locked, as long as the external asset dependencies for the project are not locked.
