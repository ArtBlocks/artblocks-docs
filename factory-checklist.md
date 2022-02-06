---
icon: check-circle
order: 800
description: A project checklist to walk through for Factory/Playground projects.
---

# Checklist for Factory/Playground Projects

!!!danger
Before proceeding to mainnet upload, please verify that your script behaves as expected across all major web browsers (e.g. Chrome, Firefox, Safari, etc.)
!!!

## Upload

1. Please ensure that you have reviewed and abided by our [Documentation](readme.md#documentation) and [Guidelines & Constraints](readme.md#guidelines-and-constraints). If you are assigning rarity to different things, Art Blocks strongly recommends that you use an instance of the Random class found [here](readme.md#safely-deriving-randomness-from-the-token-hash) to feed all of your project's randomness. Prior to uploading, please verify that your script meets this requirement.
2. Ensure your wallet is funded with enough ETH to pay the gas fees for the upload and unpausing process. For more information on the estimated cost of these steps, [click here.](readme.md#cost)
3. Submit one field at a time. Wait for that transaction to clear before attempting the next field.
4. When you upload your script, please copy it exactly from testnet.
5. Include the following in the Project Base URI field: `https://api.artblocks.io/token/`
   * **Important:** If you are setting this field for a PBAB project, rather than an Art Blocks project directly, the `baseTokenURI` field should follow a slightly different structure. Please see the [PBAB documentation](powered-by-art-blocks-pbab-onboarding/adding-new-project-shells.md) for more info.
6. As [noted in the main documentation overview](readme.md), please ensure that you are only setting a currency address if you are using some custom ERC20-compatible token (e.g., DAI) for the sale of your work. This field **should not** be set if you are accepting ETH as your payment type.
7. Please double-check, triple-check, and then check again the generated [features script](readme/features.md) results on staging to ensure they are 100% accurate. This is **extremely important** to get right, as it changes to fix any bugs you may introduce in this script may have massive impact on how the artwork is perceived by collectors and may cause confusion in the secondary market. It is **your responsibility** to guarantee that your features script is properly verified in the artist staging environment.

## Features

1. Please see [Features](creator-onboarding/features.md) for full details on how you set your project features as an artist.
2. The features script for your project should first be tested on the Ropsten testnet (https://artist-staging.artblocks.io), alongside your art script. Ensure that your features are being displayed as expected on testnet before proceeding to project deployment to mainnet.
3. When uploading your feature script to mainnet (https://www.artblocks.io/), please ensure that you are uploading the exact same features script, taking the same care that you would with your art script itself.
4. While the features script _is not_ stored on-chain like the art script is, bugs in your features script will cause meaningful disruptions for collectors trying to explore your work on a per-feature basis.

## Economics

1. Consider the overall economics of your project for a successful release.
2. Artists can only have one active project at a time.
3. As a note, we require artists to take a 2 month cooldown period between Playground and Factory drops. The cooldown period begins when your project sells out (i.e. when minting is 100% complete).

## Charity Component

* To maintain our commitment to charitable giving, we ask all artists to donate 25% of all sales above 0.25 ETH to a charity of your choice. Once the price drops below 0.25 ETH, the charity component is optional. If this applies to your works, please determine your charity of choice before mint #0.
* To whom and how you donate is up to you. If you are a single artist, you may use the additional payee field to manage on-chain donations. All revenue can also be routed to a single wallet and donated after your drop. We highly recommend consulting with a tax professional to understand your local tax liability, especially if you plan to personally receive all funds before donating.
* To find a list of charities that accept crypto donations, you can ask for advice in [!badge #artist-general] and check the pinned messages for a charity guide.

## Mint #0

1. **Before** minting mint #0, ensure that your "additional payee wallet" has been set for the same configuration that you will use it for in your project release. E.g., if you are using the "additional payee wallet" field to donate to charity at the time of mint, you must set this before minting your #0. This is done to ensure that this full functionality is tested end-to-end as part of the mint #0 process, and that there are no issues with the wallet selected for the additional payee.
2. Once your project information has been uploaded, please confirm that you're ready for mint #0.
3. Mint #0 should occur at least 48 hours in advance of your scheduled release.

## Scheduling

* Once mint #0 and the features script are in place, Art Blocks will work with you to schedule/announce your release.
* After your project has been scheduled, you are free to announce and promote your project on your social media.

## Ropsten
Once scheduled, you will have the option to make your Ropsten shell public to collectors. To help collectors easily differentiate Ropsten shells from live projects and also ensure consistency in price and series size across your shells, please do the following prior to making your Ropsten public:
1. Add [Sample Outputs] as a prefix to your project title. The formatting of your Ropsten title will be "[Sample Outputs] Project Name"
2. Adjust your price information in Ropsten to be the same as on mainnet
3. Adjust your max invocations in Ropsten to be the same as on mainnet

## Unpausing

* When it's time, you'll click the Unpause button under the Danger tab.
* When unpausing the project, please send in the tx 30 seconds prior to the top of the hour. To unpause the project, please send high gas (2-3x what is suggested as high gas on https://etherscan.io/gastracker). If you have questions about what you should set your gas to, please ask in your project DM and the Art Blocks Team can advise.
* Once the transaction clears, your project will be live for minting.

## If Dutch Auction

* Dutch auction prices will need to be manually changed by the artist every 5 minutes. To change the token price during a dutch auction, you will need to adjust the 'price per token' field and click Submit.
* If using a dutch auction drop mechanic, send in the tx 30 seconds before the 5 minute mark. You will want to use 2x or more what is suggested as high gas on https://etherscan.io/gastracker), but please keep an eye on gas as there are times when gas can spike, in which case you will need to speed up the tx. If you have questions about what you should set your gas to, please ask in your project DM and the Art Blocks Team can advise.
* If charity information is entered as an additional payee field and you would like to remove this information prior to decreasing your tier below 0.25 ETH, please adjust the additional payee field to either 0x0000000000000000000000000000000000000000 or to your own wallet address and adjust the additional payee percentage to 0% before submitting the next price tier.

## Rarities

* Do not discuss odds or feature rarities about your project until it is completely sold out.

## Finishing Steps

1. Once your project is completely sold out, you may reset the Additional Payee Percentage to 0% for any charitable giving that was conducted during minting. You're also more than happy to keep them up. If removing, you will need to edit the secondary payee info to your wallet or set the percentage to 0%
2. You may also remove any language from your Project Description that was specifically included to describe sales mechanics.
3. Report final charity donation totals to @Druid.eth
4. [For Playground projects only] Please fill out the appropriate form to add bot-support to your Discord channel for your completed project: https://github.com/ArtBlocks/artbot/issues/new/choose.
