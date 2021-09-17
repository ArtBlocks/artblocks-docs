# Checklist for Factory/Playground Projects

## Upload
- Submit one field at a time. Wait for that transaction to clear before attempting the next field.
- When you upload your script, please copy it exactly from testnet.
- Include the following in the Project Base URI field: `https://api.artblocks.io/token/`

## Economics
- Consider the overall economics of your project for a successful release.
- Artists can only have one active project at a time.
- There is a two month cooling period between the end of one project and the start of the next.

## Mint #0
- Once your project information has been uploaded, please confirm that you're ready for mint #0.

## Features
- Please see [FEATURES.md](https://github.com/ArtBlocks/artblocks-docs/blob/main/FEATURES.md) for full details on how you set your project features as an artist.
- The features script for your project should first be tested on the Ropsten testnet (https://artist-staging.artblocks.io/), alongside your art script. Ensure that your features are being displayed as expected on testnet before proceeding to project deployment to mainnet.
- When uploading your feature script to mainnet (https://beta.artblocks.io/), please ensure that you are uploading the exact same features script, taking the same care that you would with your art script itself. 
- While the features script _is not_ stored on-chain like the art script is, bugs in your features script will cause meaningful distruptions for collectors trying to explore your work on a per-feature basis.

## Scheduling
- Once mint #0 and the features script are in place, you may schedule/announce your release.

## Unpausing
- When it's time, you'll click the Unpause button under the Danger tab.
- Once the transaction clears, your project will be live for minting.

## Rarities
- Do not discuss odds or feature rarities about your project until it is completely sold out.

## Finishing Steps
- Once your project is completely sold out, please reset the Additional Payee Percentage to 0% for any charitable giving that was conducted during minting.
- You may also remove any language from your Project Description that was specifically included to describe sales mechanics.
- We would also appreciate it if you could report back once your charity donations have been completed so that we can log the results.
