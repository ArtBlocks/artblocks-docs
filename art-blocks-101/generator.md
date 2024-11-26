---
order: 900
description: Art Blocks Generator.
---

# Art Blocks Generator

The Art Blocks Generator combines artist scripts with token metadata to create unique generative art NFTs. This document outlines the basics of how the generator works, the structure of the token metadata, and related requirements for artist scripts.

## HTML Document

The Art Blocks Generator builds an html document that includes:

- A `tokenData` object that contains on-chain metadata for the NFT, including the token's hash and ID.
- The artist's on-chain project script
- (optional) A dependency used by the script. p5js, for example, is a common dependency.
- (optional) For flex projects, external asset dependencies from the Art Blocks Dependency Registry.

The HTML document created by the Generator may look something like the following:

```html
<html>
  <head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/p5.min.js"></script>
    <script>
      // Dependencies from the Art Blocks Dependency Registry injected here if populated in the Flex project
    </script>
    <script>
      let tokenData = {
        hash: "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
        tokenId: "42000001",
      };
    </script>
    <script>
      // Artist's script injected here
    </script>
  </head>
  <body></body>
</html>
```

!!!info
An on-chain version of he Art Blocks Generator is in development, which will allow for even more robust preservation of Art Blocks projects.
!!!

## The `tokenData` Object

The `tokenData` object is injected into the html document by the Art Blocks Generator. It contains the following fields:

```json
tokenData = {
  // 32-byte hash of the token
  hash: "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
   // tokenId = projectId * 1_000_000 + invocation
  tokenId: "1234567"
}
```

For Art Blocks Flex projects, the `tokenData` object may also include:

```json
tokenData = {
  ...
  // URL to preferred Arweave gateway
  preferredArweaveGateway: "https://arweave.net/",
  // URL to preferred IPFS gateway
  preferredIPFSGateway: "https://designator-string.mypinata.cloud/ipfs",
  // array of external asset Flex Dependencies
  externalAssetDependencies: [
    {
      // type of dependency
      dependency_type: "IPFS",
      // content identifier for the asset
      cid: "QmbxU6subfSzzpxketBhVBVCGhFBPdTSB8nCtppGZtpZGf",
      // data related to the asset (if any)
      data: null
    }
  ]
}
```

The `dependency_type` field will be one of the following values:

- `"IPFS"`
- `"ARWEAVE"`
- `"ONCHAIN"`
- `"ART_BLOCKS_DEPENDENCY_REGISTRY"`

Note that project scripts are responsible for fetching any IPFS or Arweave assets.

For "ART_BLOCKS_DEPENDENCY_REGISTRY" dependencies, the `cid` field will be the dependency's registry key, the data field will remain null, and additional script tag(s) will be injected into the html document to load the dependency.

For example, the following script tag would be injected into the html document for a dependency with the key `p5js@1.9.0`:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/p5.min.js"></script>
```

> If a dependency has been uploaded to the Art Blocks Dependency Registry, the on-chain generator will automatically inject the appropriate script tag(s) into the html document.

## Learning More

For additional technical resources and documentation, please refer to the Technical Requirements described in the [help.artblocks.io documentation](https://help.artblocks.io/Technical-Requirements-7f9a9aaf39ea4f20b2d5b948cf08d5aa).
