# Art Blocks Features Script

## Features Overview

All feature attributes that you want you want displayed should be directly generated from the transaction hash and should not depend on any other randomness. 

This function should essentially encapsulate the feature-determining logic within rendering script but without any library dependencies (e.g. p5js) present (the server won't have access to them). 

The function should assume that it receives the `tokenData` object as an input (containing both a `tokenId` and `hash` string), and should use these to return the correct desired feature metadata for a given mint. 

Properly displaying your project features requires both a a) feature calculation script and b) setting the feature fields for your project in the Art Blocks website's artist interface.

Updating the features script or features fields for a given project will recalculate features for all tokens within that project.

## Features Script Interface

**Important Note:** All code required for calculating your features (including any necessary helper functions) must be defined and implemented _within_ the single top-level `calculateFeatures` function.


```js
/**
 * Calculate features for the given token data.
 * @param {Object} tokenData
 * @param {string} tokenData.tokenId - Unique identifier of the token on its contract.
 * @param {string} tokenData.hash - Unique hash generated upon minting the token.
 */
function calculateFeatures(tokenData) {
  /** 
   * Implement me. This function should return a set of features in the format of key-value pair notation.
   * 
   * For example, this should return `{"Palette": "Rosy", "Scale": "Big", "Tilt": 72}` if the desired features for a mint were:
   * - Palette: Rosy
   * - Scale: Big
   * - Tilt: 72
   */
  return {}
}
```

## Features Fields

In order for filtering and rarity (% occurence of different features) to be accessible via the Art Blocks website, the feature fields must be added in the artist interface UI on the Art Blocks website.

There are two types of feature fields: `enum` and `number`:

- For `enum` fields, values should be outputted as strings in your features scripts.
- For `number` fields, the step size set in the feature fields is used for the step size of the slider in the filters.
- If there are only a few specific number values expected to be output, an artist might want to use an `enum` field and output the enumerated possible numeric values as strings (e.g. if the slider UI would *not* be the best way to navigate these features).

## Migration From Features Array

Previously the features for a given project were defined in a less structured way, via a script that could set a given array of features (e.g. `["Palette: Rosy", "Scale: Big", "Tilt: 72"]`) to a globally available `features` array. 

This process is being standardized for the Art Blocks V2 website and token API, which may require some involvement from artists to migrate old projects in alignment with their desires. 

To simplify this process, Rev Dan Catt has provided an amazing tool to generate a features script with the new format based on the features of existing projects, which you can find at `https://rarity.guide/project/{ProjectNumber}/featurescript` (where `{ProjectNumber}` is swapped out with your project of interest).

This tool is being used to assist the Art Blocks team in attempting to automatically migrate projects, but if you are an artist with an existing project that needs to or would like to modify the output of this automated result, Rev Dan's script is a great starting place.

## Additional Notes

For future projects (that have not yet minted out, which is necessary for Rev Dan's automated migration approach), it is necessary that this data be determined based on the `tokenData` itself rather than just mapping the `tokenId` to a given existing set of features as the features cannot be known until time of mint (unless all named features are purely based on the `tokenId` and not the `hash`).
