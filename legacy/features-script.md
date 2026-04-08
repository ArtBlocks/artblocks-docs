---
order: 900
description: Legacy calculateFeatures() approach for defining token traits — superseded by window.$features.
---

# Legacy: Features Script

!!!warning
This approach is no longer recommended for new projects. All new Art Blocks projects should use `window.$features` to define token traits. See [Building Your Project](/creator-onboarding/artists/1-building-your-project/) for the current approach.
!!!

The `calculateFeatures()` function was an earlier approach to defining token features on Art Blocks. It is documented here for artists with existing projects that use this pattern.

---

## How It Worked

Artists defined a `calculateFeatures(tokenData)` function in their script. Art Blocks' infrastructure called this function after the script executed, passing in `tokenData`, and used the return value to index token traits.

```javascript
// Legacy approach — for reference only
function calculateFeatures(tokenData) {
  // Re-initialize the PRNG from the hash to get consistent values
  const rand = new Random(tokenData.hash); // using the Random class below

  const palette = rand.random_choice(["Midnight", "Flame", "Ocean"]);
  const density = rand.random_int(10, 90);

  return {
    Palette: palette,
    Density: density,
  };
}
```

**Key differences from `window.$features`:**
- The function was called by Art Blocks' server-side infrastructure, not the browser
- It received `tokenData` as an argument, requiring the PRNG to be re-initialized from the hash
- The function signature was required to be exactly `calculateFeatures(tokenData)`

---

## PRNG in the Features Script

The `calculateFeatures()` function must use the same pseudo-random number generator (PRNG) as the art script, seeded from `tokenData.hash` in the same way and called in the same order. This ensures that the features returned by `calculateFeatures()` are consistent with the actual visual output of the project.

---

## Feature Field Configuration

In the old system, artists also configured "Feature Fields" in the Creator Dashboard — metadata describing each feature key (display name, type, options). This configuration was separate from the script.

---

## Migration to `window.$features`

If you're migrating an existing project from `calculateFeatures()` to `window.$features`:

1. Move your feature computation into the main script body (not a separate function)
2. Assign the result to `window.$features` synchronously at the top level
3. Remove the `calculateFeatures` function
4. Ensure the PRNG call order is consistent with your existing script

The `window.$features` assignment should produce the same trait values as your `calculateFeatures()` function for any given hash, to preserve trait consistency for already-minted tokens.

Contact Art Blocks in `#artist-tech` on Discord if you need assistance with migration.
