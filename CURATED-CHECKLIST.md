# Checklist for Curated Projects

## Upload
- Submit one field at a time. Wait for that transaction to clear before attempting the next field.
- When you upload your script, please copy it exactly from testnet.
- Include the following in the Project Base URI field: `https://api.artblocks.io/token/`
- As [noted in the main documentation overview](https://github.com/ArtBlocks/artblocks-docs/blob/main/README.md#token), please ensure that you are only setting a currency address if you are using some custom ERC20-compatible token (e.g., DAI) for the sale of your work. This field **should not** be set if you are accepting ETH as your payment type.
- Please double-check, triple-check, and then check again the generated [features script](https://github.com/ArtBlocks/artblocks-docs/blob/main/FEATURES.md) results on staging to ensure they are 100% accurate. This is **extremely important** to get right, as it changes to fix any bugs you may introduce in this script may have massive impact on how the artwork is percieved by collectors and may cause confusion in the secondary market. It is **your responsibility** to gauruntee that your features script is properly verified in the artist staging environment.

## Scheduling
- Art Blocks will work with you to schedule your curated release.

## Mint #0
- **Before** minting mint #0, ensure that your "additional payee wallet" has been set for the same configuration that you will use it for in your project release. E.g., if you are using the "additional payee wallet" field to donate to charity at the time of mint, you must set this before minting your #0. This is done to ensure that this full functionality is tested end-to-end as part of the mint #0 process, and that there are no issues with the wallet selected for the additional payee.
- Once your project information has been uploaded, please confirm that you're ready for mint #0.
- Mint #0 should occur at least 48 hours in advance of your scheduled release.

## Features
- Please see [FEATURES.md](https://github.com/ArtBlocks/artblocks-docs/blob/main/FEATURES.md) for full details on how you set your project features as an artist.
- The features script for your project should first be tested on the Ropsten testnet (https://artist-staging.artblocks.io/), alongside your art script. Ensure that your features are being displayed as expected on testnet before proceeding to project deployment to mainnet.
- When uploading your feature script to mainnet (https://beta.artblocks.io/), please ensure that you are uploading the exact same features script, taking the same care that you would with your art script itself. 
- While the features script _is not_ stored on-chain like the art script is, bugs in your features script will cause meaningful distruptions for collectors trying to explore your work on a per-feature basis.

## Unpausing
- When it's time, you'll click the Unpause button under the Danger tab.
- Once the transaction clears, your project will be live for minting.

## Rarities
- Do not discuss odds or feature rarities about your project until it is completely sold out.

## Finishing Steps
- Once your project is completely sold out, please reset the Additional Payee Percentage to 0% for any charitable giving that was conducted during minting.
- You may also remove any language from your Project Description that was specifically included to describe sales mechanics.
- We would also appreciate it if you could report back once your charity donations have been completed so that we can log the results.
- Finally, please fill out the appropriate form to add bot-support to your Discord channel for your completed project: https://github.com/ArtBlocks/artbot/issues/new/choose
