---
order: -200
description: A project checklist to walk through for Presents projects.
---

# Checklist for Presents Projects

!!!danger
Before proceeding to mainnet upload, please verify that your script behaves as expected across all major web browsers (e.g. Chrome, Firefox, Safari, etc.) We recommend using [Browserstack](https://www.browserstack.com/) to test across devices. If you do not already have an account, select Get started free and set up a free account.
!!!

## Upload

1. Please ensure that you have reviewed and abided by our [Documentation](readme/readme.md#documentation) and [Guidelines & Constraints](readme/readme.md#guidelines-and-constraints). If you are assigning rarity to different things, Art Blocks strongly recommends that you use an instance of the Random class found [here](readme/readme.md#safely-deriving-randomness-from-the-token-hash) to feed all of your project's randomness. Prior to uploading, please verify that your script meets this requirement.
2. Ensure your wallet is funded with enough ETH to pay the gas fees for the upload and unpausing process. For more information on the estimated cost of these steps, [click here.](readme/readme.md#cost)
3. Submit one field at a time. Wait for that transaction to clear before attempting the next field.
4. When you upload your script, please copy it exactly from testnet.
5. Please double-check, triple-check, and then check again the generated [features script](readme/features.md) results on staging to ensure they are 100% accurate. This is **extremely important** to get right, as it changes to fix any bugs you may introduce in this script may have a massive impact on how the artwork is perceived by collectors and may cause confusion in the secondary market. It is **your responsibility** to guarantee that your features script is properly verified in the artist staging environment.

## Features

1. Please see [Features](readme/features.md) for full details on how you set your project features as an artist.
2. The features script for your project should first be tested on the Goerli testnet (https://artist-staging.artblocks.io), alongside your art script. Ensure that your features are being displayed as expected on testnet before proceeding to project deployment to mainnet.
3. When uploading your feature script to mainnet (https://www.artblocks.io/), please ensure that you are uploading the exact same features script, taking the same care that you would with your art script itself.
4. While the features script _is not_ stored on-chain like the art script is, bugs in your features script will cause meaningful disruptions for collectors trying to explore your work on a per-feature basis.

## Tags

Add relevant tags to your project. More on tags [here](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/project-form-fields-guide/).

## Economics

1. Review the Project Pricing Model for Dutch auctions [here](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/project-pricing-model/#project-pricing-dutch-auction-settings)
2. Consider the overall economics of your project for a successful release.
3. Artists can only have one active project at a time.
4. In order to submit a new project, your previous project must be closed (sold out/completed).

## Charity Component

To maintain our commitment to charitable giving, we ask artists to consider donating 25% of sales above the resting price via Dutch auction to a charity of their choice. If you elect to participate in this way, please determine your chosen charity, and confirm its eligibility, before mint #0. To whom and how you donate is entirely up to you. Art Blocks does not require you to donate any proceeds in order to engage with our platform. If you do elect to donate to a charity, it is advisable to consider whether the charity which you choose to support qualifies under United States tax law to receive tax-deductible donations. If your project designates only one primary wallet, you may use the additional payee field to manage on-chain donations. All revenue may also be routed to a single wallet and donated after your drop. We encourage you to consult with a tax professional to understand any potential tax implications of your planned giving, as these can be widely variable.

Learn more about Charitable Donation [here](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/charitable-donations/).

## Approve additional payee info for primary and secondary sales⛽

Include the wallet addresses for primary and secondary sales to be distributed. Once submitted, the details will be approved by the Art Team. If you do not have additional wallet addresses that will receive funds from primary or secondary sales you must input `0x0000000000000000000000000000000000000000` in the blank fields.

## Mint #0

1. Note: Mint #0 will be completed with the Set Price minter. If you use a fixed price, your project will be unpaused under the Danger tab right before your project’s release. Once a project using Set Price - ETH or Custom ERC20 is unpaused, it will be live for minting. If your project is sold via a Dutch auction, please set the minter to Set Price ETH with the set price as your Dutch Auction’s base price for Mint #0. Mint #0 must be left up to chance, artists cannot use tokenId to control the features of the output.
2. **Before** minting Mint #0, ensure that your "additional payee wallet" has been set for the same configuration that you will use it for in your project release. E.g., if you are using the "additional payee wallet" field to donate to charity at the time of mint, you must set this before minting your #0. This is done to ensure that this full functionality is tested end-to-end as part of the mint #0 process, and that there are no issues with the wallet selected for the additional payee. **Please note: Art Blocks does not currently support sending primary sales payments into a multi-sig contract and there are known issues when attempting to do so. While we plan to update our minting smart contracts in the near future to resolve this, multi-sig wallets should not be used for this purpose at this time.**
3. Once your project information has been uploaded, **please confirm in your artist DM that you're ready for mint #0**. The Art Blocks Team will look over your project shell and then give you the go-ahead to mint #0.
4. Mint #0 must occur before your release can be scheduled.

### Payout Details

Be sure that you've input information in all field forms. If you do not have an additional payee for primary or secondary sales, you may put `0x0000000000000000000000000000000000000000` in the field and 0% for the payee percentage.

## Initiating your Minter Suite choice

We have a variaty of minters available for you to choose from to best suit your project.

For an overview of all minters available for artists, please see the [Minter Suite](readme/minter-suite.md) page.

For more detailed instructions on how to configure your selected minter, please see the [Minter section of the Project Form Fields Guide](readme/project-form-fields-guide.md#minter) .

!!!info
If you are using the `Dutch auction - Exponential Price Decrease` (with or without settlement) or `Dutch auction - Linear Price Decrease,` you will need to unpause your project before your auction's start time. Your project can be unpaused under the Danger tab any time prior to the starting time of your auction.  We recommend unpausing projects on the morning of your release. Once unpaused, your project will be marked as “Upcoming,” and the Dutch auction will automatically begin at your start time, leaving the beginning of the auction hands-free.
!!!

## Scheduling

- Once mint #0 and the features script are in place, Art Blocks will work with you to schedule/announce your release.
- After your project has been scheduled, you are free to announce and promote your project on your social media.
- Refer to our Marketing 101 Guide [here](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/marketing101/)

## Pre-Drop Talk

Pre-Drop Talks happen on Twitter Spaces 15 minutes prior to the release of your project. A member of the Community Team will ask you a series of questions to help collectors get to know more about your creative process and the decisions behind your project. Pre-drop talks are announced on Twitter a few days before release, and you’ll be connected with the host of your talk after your project is announced in #upcoming-projects. You will receive interview questions in advance of the live show. If you do not have a Twitter account, the Community Team will explore alternative ways to host this conversation with you.

## Unpausing

- When it's time, you'll click the Unpause button under the Danger tab.
- You may unpause your Dutch auction release up to 24 hours in advance.
- For  unpausing fixed price releases, please send in the tx 30 seconds prior to the top of the hour. To unpause the project, please send high gas (2-3x what is suggested as high gas on https://etherscan.io/gastracker). If you have questions about what you should set your gas to, please ask in your project DM and the Art Blocks Team can advise.
- Once the transaction clears, your project will be live for minting.

## Rarities

- Do not discuss odds or feature rarities about your project until it is completely sold out.

## Finishing Steps

1. If you are using Settlement in your auction, after the auction has completed, you must go to `Payout Tab` and `claim revenue`.
2. Once your project is complete, you may reset the “Additional Payee Percentage” to 0% for any charitable giving conducted during minting. If removing, you will need to edit the secondary payee info to your wallet or set the percentage to 0. In order to successfully update payout details, you will need to enter information into all fields to submit the change.
3. Report final charity donation totals in your artist DM
4. Personalize your OpenSea Collection. Learn more about doing so [here](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/opensea-personalization/).
5. **[For previously Curated only]** Please fill out the appropriate form to add bot support to your Discord channel for your completed project: https://github.com/ArtBlocks/artbot/issues/new/choose.
