---
order: 450
---

# Embroidery on Art Blocks Engine

In addition to providing a browser-based live view and media files generated from your project script, Art Blocks Engine provides tools to embroider your generative artwork on garments and accessories.

## Requirements

In order to get started, you will need:

- [ ]  Testnet project shell on Art Blocks Engine
Refer to [documentation](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/engine-project-launch/) for setup instructions*
- [ ]  Embroidery machine and software drivers compatible with DST or PES files
*If you are new to embroidery, we recommend the [Brother PE800](https://www.amazon.com/dp/B07C7HNX92?tag=thesprucecrafts-onsite-prod-20&linkCode=ogi&th=1&ascsubtag=4171238%7Cne17ef55f56ef441eb2184399ae4d1dd615%7CB07C7HNX92)*
- [ ]  JavaScript utilities for manipulating SVG markup
*Clone the embroidery template repository for an example: ‣*

## Quick Start

1. [Deploy a new project shell](https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/engine-project-launch/) to your Art Blocks Engine testnet contract
2. Upload a project script that includes a global function named `generateEmbroiderySVG` that returns a string containing SVG markup for embroidery
3. Use the [Embroidery File Downloader](https://minting-api.artblocks.io/embroidery/downloader) to generate embroidery files for minted tokens

# Project Script Requirements

In addition to following the typical [guidelines and constraints](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/#guidelines-and-constraints) for Art Blocks projects, your project script should include a global function that is only used for embroidery.

## Generating SVG for Embroidery

Implement a global function with the following type signature:

```tsx
function generateEmbroiderySVG(width: number, height: number): string
```

For example, you may include a function similar to code below:

```jsx
window.generateEmbroiderySVG = function(width, height) {
  let svg = document.createElementNS("http://www.w3.org/2000/svg", "svg"),
    path = document.createElementNS("http://www.w3.org/2000/svg", "path"),
    strokeColor = "#" + tokenData.hash.substring(2, 8),
    svgWidth = width > height ? 24.0 * width / height : 24.0,
    svgHeight = height > width ? 24.0 * height / width : 24.0;

  // the embroidery machine only follows stroked paths and ignores fills
  svg.setAttribute("fill", "none");

  // the SVG viewbox should be configured with garment dimensions
  svg.setAttribute("viewBox", `0 0 ${svgWidth} ${svgHeight}`);

  // the color needs to be matched with an appropriate spool of thread loaded in the embroidery machine
  svg.setAttribute("stroke", strokeColor);

  // typically, the SVG path is generated with code - this hard-coded path is only a simple example
  path.setAttribute(
    "d",
    "M13.828 10.172a4 4 0 00-5.656 0l-4 4a4 4 0 105.656 5.656l1.102-1.101m-.758-4.899a4 4 0 005.656 0l4-4a4 4 0 00-5.656-5.656l-1.1 1.1",
  );

  // stroke line attributes are ignored by embroidery machines, but can make a design more appealing when viewed digitally
  path.setAttribute("stroke-linecap", "round");
  path.setAttribute("stroke-linejoin", "round");

  // stroke width is ignored by the embroidery machine, but relevant for human viewers
  path.setAttribute("stroke-width", "2");

  svg.appendChild(e);

  // when viewed digitally, the SVG will scale to fill the viewport (ignored by embroidery machine)
  svg.setAttribute("height", "100vh");
  svg.setAttribute("width", "100vw");

  // the function should return the SVG markup as a string
  return svg.outerHTML;
}
```

## Functional Requirements

In order to correctly generate files for embroidery, you must:

- [ ]  Implement a `generateEmbroiderySVG` global function that returns the full markup of an `<svg>` element as a string
- [ ]  *Optional:* accept a `width` and `height` parameter (millimeters) used to resize the contents of the SVG to accomodate different garment sizes
- [ ]  Render a digital-only version of the art using a separate `<svg>` or `<canvas>` that is displayed to the user and thumbnailed in token metadata (similar to any digital-only Art Blocks project)
- [ ]  Inline all libraries and code used in your project that are not configured as an on-chain dependency

## Known Limitations

- [ ]  Avoid using SVG fills - instead, to create the visual appearance of a fill, the SVG should contains the exact paths the embroidery needle should follow
- [ ]  Avoid using asynchronous code or promises inside of the `generateEmbroiderySVG` function - the function should return valid SVG markup immediately
- [ ]  Provide margins (bleed) matching the precision of the embroidery machine to improve manufacturing yield
- [ ]  Match all colors used in your design to the colors of thread available to you for embroidering

# Embroidery in Production

In addition to the typical steps required for moving an Art Blocks Engine project to mainnet, there are additional considerations for embroidery projects.

## Logistics and Fulfillment

There are three primary customer experiences enabled for embroidery on Art Blocks Engine:

1. **Drop-shipped or batched production**  
*Consider the lead times, available materials, and the process for sending files to embroidery service providers.*
2. **Live in-person pop-up events**  
*Consider space constraints and measure the amount of time required to fulfill a single embroidered object.*
3. **At-home embroidery for token holders**  
*Consider how and when you would like to provide your users with a link to download embroidery files for a project.*

## Option 1: Batched Production

To facilitate automated testing and batched production, we provide a rate-limited API for converting Art Blocks Engine projects into DST and PES embroidery files. **Note:** the API endpoints provided for batched production are rate-limited, and cannot be linked from a public web site.

For example, the following commands illustrate how you can download individual embroidery files for tokens on an Art Blocks Engine project:

```bash
#!/bin/bash

# Example of a Goerli test script DST file
curl -O -J 'https://minting-api.artblocks.io/embroidery/goerli/0x81236b5A105d3ad6B56aC41a03E1Fd8893A08859/3000000.dst'

# Example of a Goerli test script PES file
curl -O -J 'https://minting-api.artblocks.io/embroidery/goerli/0x81236b5A105d3ad6B56aC41a03E1Fd8893A08859/3000000.pes?width_mm=400&height_mm=400'

# Example using the Plottables goerli contract (currently does not work because the token isn't embroiderable)
curl -O -J 'https://minting-api.artblocks.io/embroidery/goerli/0x9B0c67496Be8c6422fED0372be7a87707e3a6F09/4000003.dst?width_mm=400&height_mm=400'

# Example using the Plottables mainnet contract (currently does not work because the token isn't embroiderable)
curl -O -J 'https://minting-api.artblocks.io/embroidery/mainnet/0xa319C382a702682129fcbF55d514E61a16f97f9c/2000001.dst?width_mm=400&height_mm=400'
```

## Option 2: Live Events

To facilitate live events, operators of a pop-up booth can use the Embroidery File Downloader on a laptop or iPad to quickly download the relevant embroidery files for a given minted token. 

[Embroidery File Downloader](https://minting-api.artblocks.io/embroidery/downloader)

## Option 3: Home Embroidery

If you would like to provide your token holders with a link to download DST or PES files of their minted tokens, please contact us for access to the API dashboard. To generate embroidery files in an S3 bucket that may be linked from a public web site, you will need to add your project in the API dashboard here: [https://minting-api.artblocks.io/admin/embroidery/embroideryproject/](https://minting-api.artblocks.io/admin/embroidery/embroideryproject/)

# References

- [https://github.com/embroidepy/vpype-embroidery/](https://github.com/embroidepy/vpype-embroidery/)
- [https://github.com/EmbroidePy/pyembroidery](https://github.com/EmbroidePy/pyembroidery)
- [10 Best Print on Demand Companies and Sites (2023)](https://www.shopify.com/blog/print-on-demand-companies)
- [The 7 Best Embroidery Machines of 2023](https://www.thesprucecrafts.com/best-embroidery-machines-4171238)
