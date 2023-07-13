---
order: 900
---

# Project Form Fields Guide

Below, you'll find a guide to all form fields and buttons within testnet and mainnet project environments.

⛽: fields with associated gas costs
📄: fields required for artist screening

## Project Page:

### Purchases Paused

The Purchases Paused button is located above `additional details` can be used to mint on both the artist staging platform and mainnet without unpausing your project. We suggest using this method to mint token #0 and mints on testnet to avoid any accidental early mints from other collectors.

### Edit Project

The Edit Project button will lead to the back end of your shell, where you will set up your project.

## Project:

### Project name ⛽📄

This is the public name of your project.

### Artist name ⛽📄

This is how your name will appear on Art Blocks. What you choose to enter here is up to your personal preference.

### Project website ⛽

This field is optional. The link entered in your project website field should lead to a place that exhibits more about your presented project or your background as an artist. This can link to a page specific to your project, your website, your Instagram, your Twitter, your GitHub, or something else.

Make sure to enter a fully defined website link, including the `https://`

### Project description ⛽📄

The project description is a key opportunity to highlight your intentions and provide an interpretative frame around how you want a viewer/collector to approach your project. If you are struggling with this element, we have a series of prompts to guide your first draft.
• Begin with a strong, clear opening sentence.

• Lead with the artistic inquiry; what questions can be prompted or answered through this work?

• How would you describe this project to someone unfamiliar with your work?

• What inspiration, color palette influences, themes, and techniques were used?

• Examine the outputs. What can the viewer see?

• Be sure to describe any interactivity features, if applicable.

• End by summarizing how the medium, outputs, and algorithm achieve your initial inquiry or concept.

### Project license ⛽

Enter the copyright license here for your art (eg. NFT License 2.0, CC BY-NC 4.0, CC BY 4.0, etc)

Art Blocks recommends selecting a license that aligns with your values as a creator.

## Token:

### Sales Notes

This describes project-specific sales mechanics.

### Charitable Giving Details

This is where you will describe the charitable giving component of your drop, if applicable. The majority of projects released on Art Blocks choose to earmark at least 25% for this giving opportunity, but the final figure is up to you. An example of a charitable giving description is: `25% of proceeds above the resting price will be donated to non-profit educational organizations in Arizona dedicated to protecting the Sonoran Desert and its Native culture.`

### Maximum invocations ⛽

This is your total project series size.

### Base uri ⛽

[Mainnet Only] If you are an artist, your project base uri field should be: https://api.artblocks.io/token/.

## Script:

### Script type ⛽📄

Select your script type and the version number of that dependency from the drop-down menu provided. Artists must define the library AND version (when applicable).

### Aspect ratio (width/height)

Your project’s outputs must be dimension agnostic, meaning they will scale seamlessly to any window size. See more on this [here](readme.md#dimensionless). This field sets the aspect ratio for image renders but does not impact an output’s live view.

While you can control the aspect ratio, you will have no control over the dimensions of the browser on which your project will be viewed.

Your aspect ratio should be a single number. This will be your token’s width divided by height. For example, if your tokens are square, your aspect ratio should be 1.

### PNG Render delay 📄

If your piece takes a certain amount of time to render fully, you can type in the render delay to let the server know when to render your output’s static images. This render time will be in milliseconds. If your algorithm is GPU intensive, and thumbnails do not render after the render delay, request `Enhanced GPU Rendering`. For accepted artists, file the request in your artist DM. For applying artists, file your request in the Art Blocks’ Discord Channel #artist-application-support.

### Canvas Mode (toggle) 📄

If checked, data is directly pulled from the `Canvas` element using `.toDataURL()` when producing static image renders. This additional rendering mode can be leveraged for projects with varying aspect ratios across different tokens.

Please note that scripts containing multiple `Canvas` elements may not render as intended.

### Generate MP4 assets (toggle) 📄

If checked, GIFs and MP4s will be generated on individual token refreshes, batch token refreshes, and new token mints. There will be a link to the MP4 under the token display component when the MP4 is created and available for that token. If checked, the MP4 render delay, MP4 duration, MP4 frame rate, and MP4 aspect ratio settings will be visible in the UI.

Please note that scripts utilizing CSS rules for transitions and animations may not render as intended.

### MP4 Render delay

The render delay in milliseconds to start animation capture for GIF and MP4 outputs.

### MP4 Duration

The total length of the MP4, between 1 and 30 seconds. Setting this does not affect GIFs, they are set to 5 seconds.

### MP4 Frame rate

The number of frames per second of the MP4. Setting this does not affect GIFs, they are set to 24 fps.

### MP4 Aspect ratio

The aspect ratio of GIF and MP4 outputs. Due to limitations with the video codec the options are 1:1, 16:9, 9:16, 3:4, and 4:3.

### Primary display format

The project's primary view asset. This setting will be reflected on token and project detail pages on Art Blocks and secondary markets. For optimized performance, select `PNG` or `MP4` for animated projects, if outputs take a long time to render.

### Thumbnail preview format

The project's thumbnail preview asset. This setting will be reflected on grid pages on Art Blocks and secondary markets. It will also be reflected in the gallery view section on project pages within Art Blocks. For the gallery view, if the chosen asset type is `MP4` or `GIF`, an `MP4` will be displayed due to the inferior resolution of `GIF` in this context. If `PNG` is selected, the gallery view will display the `PNG` asset.

### Project scripts ⛽📄

Here, you will upload your project’s script. Your features script should be separate from your project script.

Remember, tokenData.hash is a global variable in the environment this script will live in, so you do not need to define tokenData in your script, except your script will have access to it.

If your script is big, consider minifying it. There are no limits to the total script length. That said, scripts larger than 24 kilobytes will need to be broken up into segments of 24kb. Segments can be added using the "add script segment" button when uploading a script. Be aware that you will have to pay transaction gas fees proportional to the size of the script upload.

### Features

For filtering and rarity (% occurrence of different features) to be accessible via the Art Blocks website, the feature fields must be added in the artist interface UI on the Art Blocks website.

There are two types of feature fields: `enum` and `number`:

For enum fields, values should be outputted as strings in your features scripts. These should be entered as comma-delimited strings with no quotation marks.

For number fields, the step size set in the feature fields is used for the step size of the slider in the filters. This step size is set in the feature fields UI, not the script, and should be on a per-field basis.

Suppose there are only a few specific numerical values. In that case, you may want to use an enum field and output the enumerated possible numeric values as strings (e.g., if the slider UI would not be the best way to navigate these features).

### Feature script

All code required for calculating your features (including any necessary helper functions) must be defined and implemented within the single top-level `calculateFeatures` function.

For many artists, the process for writing your features script will likely entail starting with your project script, copying it into the `calculateFeatures` interface/shell found [here](features.md #features-script-interface), and then trimming it down to remove all library (e.g., p5js) references and draw functionality and instead to build the relative key-value object map for your features.

## Minter:

!!!info
For an overview of all minters available on Art Blocks, please see the [Minter Suite](minter-suite.md) page.
!!!

### Configuring Your Minter ⛽📄

Go to the Minter tab within your shell and select the ‘minter for project’ drop-down menu. From that menu, select your desired MinterSuite option. [Please note that mint #0 will be created using the Set Price- ETH option.]

Once the desired minter is selected, you will be able to input and configure your minter's pricing and other relevant information, performing any necessary transactions along the way. For help determining pricing and configuration, please see the [Minting on Mainnet](#minting-on-mainnet) section below.

### Minting on Staging

After you’ve uploaded your script and you’re ready to start minting, ensure your `minter` is set to `Set Price - ETH (V4)`. You’ll want to set your mint price at `.0` since you’re using Goerli ETH.

### Minting on Mainnet

This section provides an overview of how to configure your selected minters on mainnet. The Art Blocks team can assist and advise in determining the best type of minter and associated pricing parameters.

Based on your selected minter option, you will need to set your project price. The different pricing mechanics are outlined below.

!!!info
Note that all current production minters support the ability to limit the number of mints on that specific minter for your project. This means that multiple minters may be used sequentially for a given project.
!!!

---

**Set Price Minters (ETH | ERC20)**

The price to purchase a token is set by the artist and is the same for all purchasers.

If using an ERC20 minter, the artist will need to specify the ERC20 token address for the custom token sale.

---

**Automated Exponential Dutch Auction (with settlement | without settlement)**

!!!info
In addition to the information below, please see the [Project Pricing: Dutch Auction Settings](project-pricing-model.md) section for more information on how to determine the appropriate pricing parameters for your auction.
!!!

For exponential Dutch auctions, artists specify the `start time`, `starting price`, `ending price`, and `half-life` for price drops. These auction mechanisms aim to allow collectors to achieve price discovery on the blockchain.

Half-life is the least intuitive of the parameters. One way to determine half-life is to think of the total duration of the auction and then work backward to find the half-life at that total time. . For example:

- Consider Exponential Dutch auction was starting at 1 ETH and lowering to 0.1 ETH over 30 minutes.
- Using [this calculator](https://www.calculator.net/half-life-calculator.html), the half-life can be determined to be 9 minutes (540 seconds). This means every 9 minutes, the price would gradually be cut in half. After 9 minutes, the auction will reach 0.5, and after 18 minutes, the auction will reach 0.25. The price drops within those half-life steps will gradually lower every block until the auction ends, at which point the auction will remain constant at the ending price.

One way to think of an exponential auction is that the rate of price _percent_ decrease is constant throughout the auction.

!!!info Artist Instructions for Claiming Revenue (settlement minter only)

Artists are able to claim revenue after either:

- the project’s sell out, or
- the dutch auction reaches resting price

We ask that artists promptly collect revenue when it becomes available. To collect revenue:

- Click the `Claim Revenue` button that becomes available in your artist dashboard, which will prompt you to send a transaction
  - If the button is selected after the project has sold out, all revenue from the project will be distributed at the time of claim
  - If the button is selected after the auction reaches resting price, but before all tokens have been sold, revenue from previous purchases will be transferred. Revenue from subsequent purchases at resting price will be distributed immediately at the time of of each purchse.

!!!

---

**Automated Linear Dutch Auction**

For linear Dutch auctions, artists will specify the `starting time`, `starting price`, `ending price`, and `ending time` of the auction. The price will then linearly decrease each block over the total auction time.

---

**Set Price - ETH, Allowlisted Users Only**

Pricing of tokens on this minter is only supported as a fixed price, in ETH.

To set up an allowlist for your project:

1. Select `Set Price - ETH, Allowlisted Users Only`
2. Upload your .csv or .txt file. See info box below for more details.
3. Enter your fixed price
4. We recommend leaving the mint per wallet limit to 1 for allowlist. If you would like to adjust this, please let the Art Blocks Team know.

!!!info
Artists are responsible for crafting their allowlist and uploading a comma-separated list of ETH addresses in a .txt or .CSV file to the artist dashboard. These wallet addresses cannot be ENS names, but list the full address of the wallet. [Premint](https://www.premint.xyz/) is a super helpful tool for creating an allowlist by using social channels to reach collectors, friends, family, etc. In addition, Art Blocks hosts a [Python script](https://github.com/ArtBlocks/artblocks-community-tooling/tree/main/SnapshotABHolders) for retrieving & snapshotting either a list of all Art Blocks token holders or the token-holders of a specific project.
!!!

---

**Set Price - ETH, Token Holders Only**

Pricing of tokens on this minter is only supported as a fixed price, in ETH.

Artists may use the artist dashboard to pre-select a list of allowlisted Art Blocks or Art Blocks Engine projects, of which any valid token holders will be able to purchase for the upcoming project. Note that a "snapshot" won't apply to this minter -- after the project has been made public, users can purchase a token from any allowlisted project and mint freely.

---

## Tags

Tags are labels you can assign to your project. Users can now filter collections based on the following tags: `animated,` `interactive,` `evolving,` `audio,` and `responsive.`

You may add tags to your project in `edit project` on the `tags` button in your shell. If you’ve already released your work on Art Blocks, we encourage you to go in and add relevant tags to your project.

**animated** - moving image projects

**interactive** - projects respond to user’s input

**evolving** - project tokens develop gradually over time

**audio** - project token incorporates sound elements

**responsive** - project outputs scale to any screen size

If you have a suggested tag for your project that you would like to be considered, please post your suggestions in Discord in #artist-general.

## Payout ⛽

Projects with multiple artists can use the additional payee address field to split project payments between multiple wallets for primary and secondary sales. When a project only has one artist, the additional payee field is commonly used to manage on-chain charitable donations. The charity’s wallet can be entered in the additional payee field. The percentage entered in the additional payee field will then be directly transferred to the charity as sales are made.

!!!danger
Artists must propose changes to their payment addresses (and splits between primary/additional) for admin approval. Approval is granted before Mint #0
!!!

#### Revenue splits with multiple artists

For projects with multiple artists, we recommend using [0xSplits](https://www.0xsplits.xyz/) to split revenue among the group. Instructions on how to create a Split can be found [here](https://www.youtube.com/watch?v=P_uqQJghNAo). Once you’ve created your Split, paste the address into the additional payee field. You can also include a charitable giving donation directly in the Split.

#### Propose current artist address or add a new one

This address will have access to edit the project in Art Blocks’ staging environment.

#### Propose additional payee address for primary sales

Input collaborator’s or charity wallet address here.

#### Propose additional payee percentage for primary sales

Payout percentages are at the artist’s discretion.

#### Propose additional payee address for secondary sales

Additional address that will receive a portion of secondary sales.

#### Propose additional payee percentage for primary sales

The royalty field should be entered as a number and does not require a % symbol.

#### Understanding secondary sales

Secondary marketplaces can choose if they’d like to honor the secondary market royalty amount. Please note that OpenSea does not currently honor this field. On OpenSea, artists receive 5% of all secondary sales. Because of this, for consistency, we recommend setting your secondary market royalty to 5%. Note that all secondary details are for on-chain royalties, which OpenSea is not yet supporting (but we expect that will happen soon). For OpenSea royalties, Art Blocks will redistribute secondary sales monthly.

To learn more about royalty distributions, see [here](faqs.md#how-does-royalty-distribution-work).

## Danger:

### Artist address ⛽

This will be the wallet address you provide to us when setting up your shell. Should you need to transfer ownership, we cannot whitelist multiple wallets. Only the address entered in the artist address field will have access to the backend of your project.

This is the address that will be used for payout.

### Unpause

When it is time for your project to go live, you will press the “Unpause” button in your mainnet shell. Once the transaction clears, your project will be live for minting.

## On Tokens

### Refresh Token Image

This button will queue your token thumbnail to be refreshed. The refresh takes time to process fully. If a script update was successful, and `live views` are correct, but thumbnails haven’t refreshed, please clear your cache. If you have cleared your cache and are still not seeing the correct thumbnail view,a subgraph delay may be the reason. Stay updated on system operations at [status.artblocks.io] (status.artblocks.io).

Rendering tokens does take computing power, of which we have a limited amount. Please feel free to refresh tokens after making updates, but note that if our rendering pipeline starts clogging up requests, we may have to consider rate-limiting refresh requests. In summary, use this button when testing out updates, but avoid spamming, or things will get jammed up.

With this button, you can refresh per token. The Art BlocksTeam has the power to refresh all thumbnails in a project at once, and we are happy to do so for you. Request a batch refresh after updating your script in your artist DM. If you are still in the application queue, you may request a batch refresh in the #artist-application-support channel in Discord.

### Details

The details page is specific to each token. On the details page, you will find the token’s features and links to secondary marketplaces.

### Image

The image button will generate a PNG of the token’s thumbnail.

### Live

As a note, the live generator view will give a bad request error until the project is public. To access the live view add `/?render=true` to the end of the generator link. I.e. `https://generator-staging-goerli.artblocks.io/0x00000000000000000/46000000/?render=true`

Once a project is public, this link will function. While a project is private, live views can also be viewed on the details section of the individual token.
