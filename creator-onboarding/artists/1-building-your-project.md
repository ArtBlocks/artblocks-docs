---
order: 900
description: Technical requirements for Art Blocks generative art scripts — tokenData, PRNG, window.$features, and conversion guide.
---

# 1. Building Your Project

This page covers the technical requirements for building a generative art script for Art Blocks. Your script will be stored on-chain and run in the Art Blocks Generator — a browser-based environment that injects `tokenData` and loads your dependency library.

---

## Quick Start: MCP Scaffold

The fastest way to get started is with the Art Blocks MCP Server:

```
"Scaffold a p5.js Art Blocks project with window.$features for Palette and Density traits"
```

The `scaffold_artblocks_project` tool generates a complete `index.html` + art script with the PRNG, canvas setup, and feature stubs already wired up. Connect the MCP server in under 5 minutes — see the [Quick Start](/developer/mcp-server/quick-start/).

---

## What the Generator Provides

When your script runs, the Art Blocks Generator has already:

1. Loaded your dependency library (p5.js, Three.js, etc.) as a `<script>` tag
2. Injected a `tokenData` global with the token's hash and other metadata
3. Applied CSS for full-viewport canvas rendering

Your script runs after all of this setup is complete.

---

## `tokenData`

```javascript
let tokenData = {
  hash: "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
  tokenId: "42000001"
}
```

`tokenData.hash` is a 32-byte hex string — the unique, on-chain random seed for this token. **This is your only randomness source.**

`tokenData.tokenId` encodes both the project and invocation:
```javascript
const projectId = Math.floor(parseInt(tokenData.tokenId) / 1_000_000)
const invocation = parseInt(tokenData.tokenId) % 1_000_000
```

---

## Deterministic Randomness (PRNG)

**Never use `Math.random()` or `Date.now()` as a randomness source.** These are non-deterministic — the same token would produce different outputs on different loads, which breaks the fundamental guarantee of generative art on Art Blocks.

Instead, seed a pseudo-random number generator (PRNG) from `tokenData.hash`:

```javascript
class Random {
  constructor() {
    const hex = tokenData.hash.slice(2);
    const seeds = [
      parseInt(hex.slice(0, 8), 16),
      parseInt(hex.slice(8, 16), 16),
      parseInt(hex.slice(16, 24), 16),
      parseInt(hex.slice(24, 32), 16),
    ];
    this._state = seeds;
  }
  _next() {
    let [a, b, c, d] = this._state;
    a |= 0; b |= 0; c |= 0; d |= 0;
    let t = (((a + b) | 0) + d) | 0;
    d = (d + 1) | 0;
    a = b ^ (b >>> 9);
    b = (c + (c << 3)) | 0;
    c = (c << 21) | (c >>> 11);
    c = (c + t) | 0;
    this._state = [a, b, c, d];
    return (t >>> 0) / 4294967296;
  }
  random_dec()             { return this._next(); }
  random_num(a, b)         { return a + this._next() * (b - a); }
  random_int(a, b)         { return Math.floor(a + this._next() * (b - a + 1)); }
  random_bool(p)           { return this._next() < p; }
  random_choice(arr)       { return arr[Math.floor(this._next() * arr.length)]; }
}

const R = new Random();
```

---

## Token Features with `window.$features`

Token features (traits) are defined by assigning an object to `window.$features` in your art script. Art Blocks reads this value to index token traits.

```javascript
// Compute your traits using the PRNG
const palette = R.random_choice(["Midnight", "Flame", "Ocean", "Forest"]);
const density = R.random_int(10, 90);
const animated = R.random_bool(0.3);

window.$features = {
  Palette: palette,
  Density: density,
  Animated: animated,
};
```

**Rules:**
- Values must be deterministic: the same hash (and PostParam settings) must always produce the same features
- For numeric traits, use consistent decimal precision

The legacy `calculateFeatures()` function approach is no longer documented here — see [Legacy: Features Script](/legacy/features-script/) if you have an existing project using that approach.

---

## Resolution Agnosticism

Art Blocks tokens are rendered at different sizes — from thumbnails to large displays. Your script must be **resolution agnostic**: it should fill the viewport at any size, using relative coordinates rather than fixed pixel dimensions.

For p5.js:

```javascript
function setup() {
  createCanvas(windowWidth, windowHeight);
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```

For vanilla JS / canvas:

```javascript
const canvas = document.querySelector("canvas");
function resize() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
  draw(); // redraw on resize
}
window.addEventListener("resize", resize);
resize();
```

Coordinate all drawing relative to `canvas.width` and `canvas.height`, not hardcoded values.

---

## Script Requirements

| Requirement | Detail |
|---|---|
| **Single script file** | One JavaScript file only |
| **Single dependency** | One library (p5.js, Three.js, etc.) from the approved list |
| **No CDN script tags** | The generator injects the library — do not add `<script>` tags |
| **No `Math.random()`** | Use `tokenData.hash`-seeded PRNG for all randomness |
| **No DOM setup** | No `<canvas>` creation — the generator provides a `<canvas>` element |
| **Resolution agnostic** | Must render correctly at any viewport size |
| **Deterministic** | Same hash → same output, always |

### Supported Libraries

All libraries must be from the Art Blocks Dependency Registry. Current supported libraries include:

- **p5.js** — v1.0.0, v1.9.0, v1.11.11
- **Three.js** — v0.124.0, v0.160.0, v0.167.0
- **regl** — v2.1.0
- **Tone.js** — v14.8.15
- **Paper.js** — v0.12.15
- **Babylon.js** — v5.0.0, v6.36.0
- **A-Frame** — v1.2.0, v1.5.0
- **Vanilla JS** — no dependency (canvas, WebGL, SVG)

For the full list including all versions and notes, see [Supported Script Types & Dependency Versions](/protocol/on-chain-generator/#supported-script-types--dependency-versions).

---

## Rendering Environment

Static images are rendered for all projects (used as thumbnails, on OpenSea, etc.). Art Blocks uses compute instances running headless Chromium with [Puppeteer](https://github.com/puppeteer/puppeteer). Headless Chromium requires the use of [SwiftShader](https://swiftshader.googlesource.com/SwiftShader/+/HEAD/docs/Index.md), a CPU implementation of the GPU API. This means GPU-intensive projects will render slower and may require optimization.

To closely replicate this environment while developing, use Chrome and turn **off** "Use Hardware Acceleration" in Settings.

---

## Local Development

Set up a local `index.html` that mirrors the generator environment:

```html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/p5.min.js"></script>
  <script>
    let defined_hash = new URLSearchParams(window.location.search).get("hash");
    let tokenData = {
      tokenId: "0",
      hash: defined_hash || "0x" + Array.from({length: 64}, () =>
        "0123456789abcdef"[Math.floor(Math.random() * 16)]).join(""),
    };
  </script>
  <style>
    html { height: 100%; }
    body { min-height: 100%; margin: 0; padding: 0; }
    canvas { padding: 0; margin: auto; display: block; position: absolute;
             top: 0; bottom: 0; left: 0; right: 0; }
  </style>
</head>
<body>
  <canvas></canvas>
  <script src="sketch.js"></script>
</body>
</html>
```

Test with specific hashes by appending `?hash=0x...` to the URL. Test with many different hashes to ensure variety and that no hash causes errors.

For a code template to start from, see the [Art Blocks Starter Template](https://github.com/ArtBlocks/artblocks-starter-template) or the [scaffold art script skill](/developer/mcp-server/skills/#available-skills).

---

## Script Upload Cost

Uploading your script to Ethereum costs gas. To estimate the cost:

```
Cost (ETH) = 235 × bytes × gwei_price × (1 / 1,000,000,000)
```

For example, a 10 KB script at 1 gwei:

```
235 × 10,000 × 1 × (1 / 1,000,000,000) = 0.00235 ETH
```

Artists typically target 5–20 KB for their scripts (excluding the library). To reduce size: maximize code reuse with functions, remove comments, and minify finished code. Check [etherscan.io/gastracker](https://etherscan.io/gastracker) for current gas prices before uploading as prices can vary significantly.

---

## Conversion Guide: Adapting an Existing Sketch

If you have an existing p5.js or vanilla JS sketch that you want to convert to Art Blocks format:

1. **Replace `Math.random()`** with calls to your `Random` class PRNG seeded from `tokenData.hash`
2. **Remove CDN `<script>` tags** — the generator loads your library automatically
3. **Remove canvas creation code** — for p5.js, remove `createCanvas()` calls or use `windowWidth`/`windowHeight`; for vanilla JS, select the existing `<canvas>` instead of creating one
4. **Make dimensions relative** — replace hardcoded pixel values with percentages of `width`/`height`
5. **Add `window.$features`** — compute and assign your token traits synchronously
6. **Verify determinism** — reload the same `?hash=` URL multiple times and confirm identical output

For a full step-by-step conversion walkthrough, use the MCP's `scaffold_artblocks_project` tool or read the [Generator Specification](artblocks://generator-spec) resource available via the MCP server.

---

## Testing Checklist

Before submitting for review:

- [ ] Script runs without errors in Chrome, Firefox, and Safari
- [ ] Same hash always produces identical output (deterministic)
- [ ] Different hashes produce meaningfully different outputs
- [ ] No hardcoded pixel dimensions — scales at all viewport sizes
- [ ] No use of `Math.random()` or `Date.now()` for randomness
- [ ] `window.$features` is assigned synchronously with correct values
- [ ] Script is a single file with a single dependency (or no dependency)
- [ ] No CDN `<script>` tags in the script
- [ ] Tested across at least 20–40 different hashes
- [ ] Script locks up or errors for no hash value (test edge cases)
