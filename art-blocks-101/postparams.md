---
order: 800
description: PostParams
---

# PostParams

PostParams are a technology that allow generative tokens to evolve over time while still preserving core artistic intent.

Configurable parameters are stored on the blockchain, and can be updated over time. A project's artist decides what PostParams exist, how they can be changed, and who can make changes.

## Creative Possibilities

PostParams opens up a wide range of creative avenues for generative artists and collectors alike:

- **Collector Customization**: Allow collectors to toggle between color palettes, visual styles, or animation behaviors within artist-defined parameters.
- **Artist-Collector Collaboration**: Create works where both artist and the collector have specific controls, establishing a collaborative relationship.
- **Physical Art Connections**: Enable collectors to configure PostParams before the physical production of artworks, creating a bridge between digital and physical realms.
- **Living Artworks**: Design pieces that evolve over time through interactions or changing parameters, telling an ongoing story.
- **Network Effects**: Enable multiple token owners to influence different aspects of related artworks, creating community-driven, networked experiences.

**Future Development**:

- **Real-World Data**: Design art that reacts to on-chain data like ETH price, wallet address, or other external inputs.

_Note: Please reach out to the Art Blocks team if you would like to explore reacting to live, on-chain data. We are happy to help you brainstorm your creative ideas._

# How-To Guide

## Video Tutorial

https://www.youtube.com/embed/4-_KgVZRVJs

Video Notes and References:

- PostParams Example in video: [https://github.com/ryley-o/post-param-example](https://github.com/ryley-o/post-param-example)
- Creator Dashboard: [https://create.artblocks.io/](https://create.artblocks.io/)
- Artist Staging Token Link Example: [https://artist-staging.artblocks.io/token/0x12f976648178b0c37e7b7ab218059b12b29dc78d/21000000](https://artist-staging.artblocks.io/token/0x12f976648178b0c37e7b7ab218059b12b29dc78d/21000000)
  - Note: Artists may directly navigate to their tokens' links by modifying the contract address and/or token id in the example url above. This allows the artist to preview their token's PostParam editing experience without requiring project activation.

## Configuring project as artist

As an artist, the creator dashboard (create.artblocks.io) is the easiest way to configure your project's PostParams. The creator dashboard allows you to configure the following:

- Parameter names
- Parameter values
- Parameter types
- Parameter constraints/limits
- Parameter lock dates

Note that if you would like your PostParams to show up as feature overrides, using the same parameter name as a feature name will properly override the feature.

## Configuring token as collector

Token owners may log into the artblocks.io website and configure PostParams for their token on the token's page. The website will display a preview of the token with edited values, allowing collectors to preview the changes before forever registering the changes on the blockchain as part of the token's provenance. The connected wallet must have authority to change parameters for the token, or be a valid delegate for the token on delegate.xyz v2.

# Technical Overview

## Compatibility

Recent Art Blocks Engine Flex NFTs (core version v3.2.5+) support configurable PostParams. If you would like an updated core contract, please contact the Art Blocks team.

## Supported parameter types

- Enum
- Boolean
- Integer Number Range
- Decimal Number Range
- Color
- Timestamp (1970+)
- String

## Supported Authorization Methods

- Artist
- Token Owner
- Address/Smart Contract

## Supported Parameter Constraints

- Min
- Max
- Lock date

## Accessing PostParams in project script

PostParams are injected using the typical Art Blocks Generator's `tokenData` object in a Flex Dependency's data field.

The following is a simple example of how to access an integer parameter in your project script:

```javascript
// Typically, the first external asset dependency is the PostParam.
// You can check your project configuration on Art Blocks Creator Dashboard
// under Scripts => Flex Assets, and the PostParam asset will show up as the
// external asset dependency with text "#web3call-contract#"
const pp = tokenData.externalAssetDependencies[0];

// helper function to parse PostParam integer values, or fallback
// to the token-hash-based value if the PostParam value is not set
function getPpInt(ppVal, hashBasedVal) {
  const n = parseInt(ppVal);
  return isNaN(n) ? hashBasedVal : n;
}

// accessing a PostParam named "NumShapes"
const amountMoving = getPpInt(
  pp?.data?.["NumShapes"], // prioritize the PostParam value if defined
  R.random_int(0, 100) // R is the hash-based pseudorandom number generator
);
```

The following is a more complete example of how to access multiple PostParams of different types in your project script.

```javascript
// Palettes are defined in the script, as well as in the PostParam Configuration as an enum
let palettes = [
  {
    name: "Midnight Citrus",
    colors: ["#0f0f1c", "#ffcc00", "#ff7f11", "#ffa69e", "#4d194d"],
  },
  {
    name: "Electric Bloom",
    colors: ["#8ecae6", "#219ebc", "#023047", "#ffb703", "#fb8500"],
  },
  {
    name: "Forest Neon",
    colors: ["#073b3a", "#0b6e4f", "#08a045", "#d4d700", "#fdfcdc"],
  },
];

// Typically, the first external asset dependency is the PostParam.
const pp = tokenData.externalAssetDependencies[0];

// helper function to parse PostParam integer values, or fallback
// to the token-hash-based value if the PostParam value is not set
function getPpInt(ppVal, hashBasedVal) {
  const n = parseInt(ppVal);
  return isNaN(n) ? hashBasedVal : n;
}

// helper function to parse boolean values from PostParam strings, or fallback
// to the token-hash-based value if the PostParam value is not set
function parsePpBool(ppVal, hashBasedVal) {
  if (ppVal === "true") return true;
  if (ppVal === "false") return false;
  // if undefined, return hashBasedVal
  return hashBasedVal;
}

// --- ACCESSING VARIOUS PostParams ---

// get enum PostParam "Palette", fallback to hash-based random choice
const hashBasedPalette = R.random_choice(palettes);
const palette =
  palettes.find((p) => p.name === pp.data["Palette"]) || hashBasedPalette;

// get boolean PostParam "Animate", fallback to hash-based random boolean
const animate = parsePpBool(pp?.data?.["Animate"], R.random_dec() < 0.5);

// get integer PostParam "NumShapes", fallback to hash-based random integer
const numShapes = getPpInt(
  pp?.data?.["NumShapes"], // prioritize the PostParam value if defined
  R.random_int(10, 100) // hash-based fallback
);

// get color PostParam "BackgroundColor", fallback to white
const backgroundColor = pp?.data?.["BackgroundColor"] ?? "#ffffff";

// get timestamp PostParam "Birthday", fallback to null
const birthdayTimestamp = pp?.data?.["Birthday"] ?? null;

// get string PostParam "Name", fallback to null
const name = pp?.data?.["Name"] ?? null;

// --- END ACCESSING PostParams ---
```

## PostParams as token features

Token features, for example `type: bold` on the Chromie Squiggle, are a way to enrich your tokens with artist-specified metadata.

PostParams may be used as token features, and will override the feature if a PostParam with the same name exists.

For example, if you have a feature named `Color` and a PostParam named `Color`, the PostParam will override the feature's value after it is configured. Upon each re-configuration, the token's features will be updated to match the configured PostParam value.

Additionally, PostParams will be injected into a project's features script, allowing the features script to translate from a PostParam to whatever feature is desired. This enables more complex parsing and translation of PostParams to features that the more simple by-name override method cannot. The `tokenData` object in the features script contains external asset dependencies in the same format as the `tokenData` object in the project script.

## Updating PostParams

PostParams may be updated at any time, provided the connected wallet has authority to change PostParams for the token, or is a valid delegate for the token on delegate.xyz v2. The parameter must also not be locked (see next section).

## Locking PostParams

Artists may configure a parameter to be locked at a specific date and time, at the project level. Once the parameter is locked, it may never be unlocked, cementing the parameter value at the time of locking.

## Hooks and Live Data

The PostParam system is designed to be extensible to allow for live data hooks. This enables injecting any live on-chain data into the project script. This is more advanced functionality and may require some solidity coding. Please reach out to the Art Blocks team if you would like to explore ideas in this area.

The Art Blocks team has published a few examples of live data hooks in the [Art Blocks Contracts GitHub repository](https://github.com/ArtBlocks/artblocks-contracts/tree/main/packages/contracts/contracts/web3call/augment-hooks). Examples include:

- injecting token owner's address and ETH balance
- injecting the price of Ethereum
- injecting Chromie Squiggle's floor price
- injecting block parameters such as gas price
- injecting the result of a chainlink oracle

Configuring hooks is not currently available in the creator dashboard, but can be easily configured with tools like etherscan. Please reach out to the Art Blocks team if you would like to explore this.
