---
order: 800
description: How the Art Blocks Generator assembles generative art from on-chain data.
---

# The Art Blocks Generator

The Art Blocks Generator combines artist scripts, token hashes, and dependency libraries into a complete, browser-viewable HTML document — entirely from data stored on the blockchain. This document explains how it works, the structure of the `tokenData` object, and related requirements for artist scripts.

For the full technical specification for building Art Blocks projects, see the [Art Blocks Generator Specification](https://mcp.artblocks.io/mcp) resource (`artblocks://generator-spec`) available via the MCP server.

---

## HTML Document Structure

The Generator builds an HTML document that includes, in order:

1. Dependency Registry script tags (if any registered deps are configured as FLEX dependencies)
2. The library CDN script tag for the project's chosen library (p5.js, Three.js, etc.), or an import map for module-based libraries
3. The `tokenData` object injection
4. CSS styles for full-viewport canvas rendering
5. A `<canvas>` element (for vanilla JS projects)
6. The artist's on-chain project script

The resulting HTML looks roughly like:

```html
<html>
  <head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/p5.min.js"></script>
    <script>
      let tokenData = {
        hash: "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
        tokenId: "42000001",
        externalAssetDependencies: [],
        preferredIPFSGateway: "https://ipfs.artblocks.io/ipfs/",
        preferredArweaveGateway: "https://arweave.net/"
      };
    </script>
    <style>
      html { height: 100%; }
      body { min-height: 100%; margin: 0; padding: 0; }
      canvas { padding: 0; margin: auto; display: block; position: absolute; top: 0; bottom: 0; left: 0; right: 0; }
    </style>
  </head>
  <body>
    <canvas></canvas>
    <script>
      /* Artist's script injected here */
    </script>
  </body>
</html>
```

**Key guarantee:** By the time the art script executes, all library dependencies are loaded and available, and `tokenData` is fully populated.

---

## The `tokenData` Object

The `tokenData` object is a global injected before the art script runs. For standard projects:

```javascript
let tokenData = {
  // 32-byte hex hash — the primary source of randomness
  hash: "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
  // tokenId = (projectId * 1_000_000) + invocationNumber
  tokenId: "42000001"
}
```

For Engine Flex projects with external dependencies, `tokenData` also includes:

```javascript
let tokenData = {
  hash: "0x...",
  tokenId: "...",
  // URL to preferred Arweave gateway
  preferredArweaveGateway: "https://arweave.net/",
  // URL to preferred IPFS gateway
  preferredIPFSGateway: "https://designator-string.mypinata.cloud/ipfs",
  // Array of FLEX external asset dependencies
  externalAssetDependencies: [
    {
      dependency_type: "IPFS",         // "IPFS" | "ARWEAVE" | "ONCHAIN" | "ART_BLOCKS_DEPENDENCY_REGISTRY"
      cid: "QmbxU6subfSzzpxketBhVBVCGhFBPdTSB8nCtppGZtpZGf",
      data: null
    }
  ]
}
```

### Dependency Types

| `dependency_type` | Description |
|---|---|
| `"IPFS"` | Content on IPFS. Script fetches using `preferredIPFSGateway + cid`. |
| `"ARWEAVE"` | Content on Arweave. Script fetches using `preferredArweaveGateway + cid`. |
| `"ONCHAIN"` | On-chain data. For PostParams, `data` contains a resolved key/value object. For BytecodeStorage, `data` contains the on-chain content string. |
| `"ART_BLOCKS_DEPENDENCY_REGISTRY"` | A library registered in the Dependency Registry. Injected as a `<script>` tag automatically — `data` is null; no manual fetch required. |

### Module-Based Libraries (Three.js v0.161+)

For module-based dependencies like Three.js v0.167.0, the generator injects an import map instead of a script tag, and wraps the art script in `<script type="module">`:

```html
<script type="importmap">
  { "imports": { "three": "https://cdn.../three.module.min.js" } }
</script>
<script type="module">
  import * as THREE from 'three'
  // artist's script
</script>
```

---

## The On-Chain Generator

The [Art Blocks On-Chain Generator](https://etherscan.io/address/0x953D288708bB771F969FCfD9BA0819eF506Ac718#readProxyContract) is a smart contract that performs the HTML assembly entirely from blockchain data. It was deployed to give Art Blocks tokens permanent, infrastructure-independent viewability.

Previously, viewing an Art Blocks piece required a centralized generator service to assemble the HTML. The on-chain generator removes that dependency: anyone can retrieve any Art Blocks artwork with a single call to the smart contract — no servers required.

The generator currently supports approximately 90% of all Art Blocks flagship projects fully on-chain, with the remaining ~10% referencing widely-distributed CDN packages.

### How It Works

The generator orchestrates three on-chain components:

- **Core Contracts** — Store the project's creative code and per-token hash data.
- **[Dependency Registry](https://etherscan.io/address/0x37861f95882ACDba2cCD84F5bFc4598e2ECDDdAF#readProxyContract)** — Manages JavaScript library dependencies; p5.js v1.0.0 and Three.js v0.124.0 are stored fully on-chain.
- **[scripty.sol](https://github.com/intartnft/scripty.sol)** — Gas-efficient on-chain HTML builder that stitches together large JS-based script tags.

### Retrieving a Token

To get the browser-viewable HTML for Chromie Squiggle #0:

1. Visit the Generator Contract on Etherscan: [0x953D288708bB771F969FCfD9BA0819eF506Ac718](https://etherscan.io/address/0x953D288708bB771F969FCfD9BA0819eF506Ac718#readProxyContract)
2. Call `getTokenHtml` with:
   - Core contract: `0x059edd72cd353df5106d2b9cc5ab83a52287ac3a`
   - Token ID: `0`
3. The returned HTML is complete and self-contained — paste it into a browser to view the artwork.

For a base64-encoded data URI (paste directly in browser address bar), call `getTokenHtmlBase64EncodedDataUri` instead.

An open-source viewer that streamlines this process is available at [github.com/ArtBlocks/on-chain-generator-viewer](https://github.com/ArtBlocks/on-chain-generator-viewer).

---

## Supported Script Types & Dependency Versions

The project's script type and dependency version are set in the Art Blocks Creator Dashboard and determine which library the generator loads. All available libraries are registered in the Art Blocks Dependency Registry.

| Script Type | Library | Versions | Notes |
|---|---|---|---|
| `js` | None (vanilla) | — | Canvas API, raw WebGL, SVG |
| `p5js` | p5.js | 1.0.0, 1.9.0, 1.11.11 | `setup()` and `draw()` called automatically |
| `threejs` | Three.js | 0.124.0, 0.160.0, 0.167.0 | v0.161+ uses ES module import maps |
| `regl` | regl | 2.1.0 | WebGL wrapper |
| `tonejs` | Tone.js | 14.8.15 | Audio synthesis |
| `svg` | None | — | SVG-based output |
| `paperjs` | Paper.js | 0.12.15 | Vector graphics |
| `zdog` | Zdog | 1.1.2 | Pseudo-3D illustration |
| `babylonjs` | Babylon.js | 5.0.0, 6.36.0 | 3D engine |
| `aframe` | A-Frame | 1.2.0, 1.5.0 | WebVR/WebXR |
| `processing` | Processing.js | 1.4.6 | Processing port |
| `custom` | User-defined | — | No wrapper template, full control |

---

## Local Development

For local development, create an `index.html` that mirrors the generator structure, with a mock `tokenData`:

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/p5.min.js"></script>
  <script>
    let defined_hash = new URLSearchParams(window.location.search).get("hash")
    let tokenData = {
      tokenId: "0",
      hash: defined_hash || "0x" + Array.from({length: 64}, () =>
        "0123456789abcdef"[Math.floor(Math.random() * 16)]).join(""),
      externalAssetDependencies: [],
      preferredIPFSGateway: "https://ipfs.artblocks.io/ipfs/",
      preferredArweaveGateway: "https://arweave.net/"
    }
  </script>
  <style>
    html { height: 100%; }
    body { min-height: 100%; margin: 0; padding: 0; }
    canvas { padding: 0; margin: auto; display: block; position: absolute; top: 0; bottom: 0; left: 0; right: 0; }
  </style>
</head>
<body>
  <canvas></canvas>
  <script src="sketch.js"></script>
</body>
</html>
```

Use the `?hash=0x...` query parameter to test with specific hashes and verify determinism across reloads.

For a complete project scaffold with PRNG, canvas setup, and `window.$features`, use the MCP `scaffold_artblocks_project` tool — see the [Building Your Project](/creator-onboarding/artists/1-building-your-project/) guide.
