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

### Project name  ⛽📄

This is the public name of your project.

### Artist name  ⛽📄
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

Select your script type and the version number of that dependency from the drop-down menu provided.  Artists must define the library AND version (when applicable).

### Aspect ratio (width/height) 

Your project’s outputs must be dimension agnostic, meaning they will scale  seamlessly to any window size. See more on this [here](readme.md#dimensionless). This field sets the aspect ratio for image renders but does not impact an output’s live view.

While you can control the aspect ratio, you will have no control over the dimensions of the browser on which your project will be viewed.

Your aspect ratio should be a single number. This will be your token’s width divided by height. For example, if your tokens are square, your aspect ratio should be 1.

### Render delay 📄

If your piece takes a certain amount of time to render fully, you can type in the render delay to let the server know when to render your output’s thumbnails. This render time will be in milliseconds. If your algorithm is GPU intensive, and thumbnails do not render after the render delay, request `Enhanced GPU Rendering`. For accepted artists, file the request in your artist DM. For applying artists, file your request in the Art Blocks’ Discord Channel #artist-application-support. 

### Display static (toggle)

If red, the project’s primary view will be dynamic; if blue, the project’s primary view will be static. These settings will be reflected on Art Blocks and secondary markets once the project is live.

For optimized performance, toggle `display static` if outputs are not animated, but take a long time to render.

### Project scripts ⛽📄
Here, you will upload your project’s script. Your features script should be separate from your project script.

Remember, tokenData.hash is a global variable in the environment this script will live in, so you do not need to define tokenData in your script, except your script will have access to it.

If your script is big, consider minifying it. There are no limits to the total script length. That said, scripts larger than 24 kilobytes will need to be broken up into segments of 24kb. Segments can be added using the plus symbol (+) when uploading a script. Be aware that you will have to pay transaction gas fees proportional to the size of the script upload.

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

### MinterSuite ⛽📄

The MinterSuite is an update to our broader smart-contract architecture at Art Blocks that allows artists to set specific minting contracts on a per-project basis.

The MinterSuite currently includes the following minter options, which will continue to expand over time:
**Set Price - ETH** is used for fixed price releases

**Automated Exponential Dutch Auction**: For exponential Dutch auctions, artists specify the starting price, ending price, and the half-life for price drops. 

**Automated Linear Dutch Auction**: For linear Dutch auctions, artists will specify the starting price, ending price, starting time, and ending time of the auction. The price will then gradually decrease each block over the total auction time.

**Set price in custom ERC20**: Set price in ERC20 is a fixed price for your sale with a custom token. Artists will specify the address for the custom token sale. 

**Set Price - ETH, Allowlisted Users Only (V2)** is used for allowing only a predetermined list of wallet addresses to mint. These wallets can mint unlimited times until the project invocations limit is reached (if no mint limit was set) or as many times as they want until they reach the mint limit. Artists can choose the list of addresses to allow as well as the # of mints allowed per-wallet. Currently, artists are responsible for crafting their allowlist and uploading a comma-separated list of ETH addresses in a .txt or .CSV file to the artist dashboard. Premint is a super helpful tool for creating an allowlist by using social channels to reach collectors, friends, family, etc. In addition, Art Blocks hosts a Python script for retrieving & snapshotting 1) all Art Blocks token holders and 2) all token-holders of a specific project (please note: this script should be updated to reflect recent changes to Art Blocks infrastructure).

**[Artists on Staging]** After you’ve uploaded your script and you’re ready to start minting, ensure your `minter` is set to `Set Price - ETH (V2)`. You’ll want to set your mint price at `.0` since you’re using Goerli ETH. 

### How to set your Project Price

You may choose between the different pricing mechanics outlined below. The first step is to choose your desired selling option. The Art Blocks team can assist and advise in determining this.

### Different Project pricing mechanics. 

**Set Price - ETH** is used for fixed price releases

**Automated Exponential Dutch Auction**: For exponential Dutch auctions, artists specify the starting price, ending price, and the half-life for price drops. An easier way to determine this is to think of the total duration of the auction and then work backward to find the half-life at that total time. This model allows collectors to decide the value of the work. For example, let's say that an Exponential Dutch auction was starting at 1 ETH and lowering to 0.1 ETH over 30 minutes. In this case, the half-life is 9 minutes. This means every 9 minutes, the price would gradually be cut in half. After 9 minutes, the auction will reach 0.5, and after 18 minutes, the auction will reach 0.25. The price drops within those half-life steps will gradually lower every block. You can use [this calculator] (https://www.calculator.net/half-life-calculator.html) to find your auction’s half-life: Please note that results from that calculator will need to be converted from minutes to seconds for Art Blocks. 

**Automated Linear Dutch Auction**: For linear Dutch auctions, artists will specify the starting price, ending price, starting time, and ending time of the auction. The price will then gradually decrease each block over the total auction time.

**Set price in custom ERC20**: Set price in ERC20 is a fixed price for your sale with a custom token. Artists will specify the address for the custom token sale. 

**Set Price - ETH, Allowlisted Users Only (V1)** these are addresses that are allowed to mint as many times as they want until they reach the mint limit (artists sets mint/wallet)

### Input your pricing information

Go to the Minter tab within your shell and select the ‘minter for project’ drop-down menu. From that menu, select your desired MinterSuite option. [Please note that mint #0 will be created using the Set Price- ETH option. If your project is sold via Dutch auction, please set the price to your auction’s resting price for mint #0. After mint #0, you may then adjust the MinterSuite back to your desired option.] Once the price option has been selected from the drop-down menu, select Submit. If you’re using a Dutch auction minter option, you will then enter the `start price in eth` and `base price in eth`.

## Tags:

Tags are labels you can assign to your project. Users can now filter collections based on the following tags: `animated,` `interactive,` `evolving,`  `audio,` and `responsive.`

You may add tags to your project in  `edit project` on the `tags` button in your shell. If you’ve already released your work on Art Blocks, we encourage you to go in and add relevant tags to your project. 

**animated** - moving image projects

**interactive** - projects respond to user’s input

**evolving** - project tokens develop gradually over time

**audio** - project token incorporates sound elements

**responsive** - project outputs scale to any screen size

If you have a suggested tag for your project that you would like to be considered, please post your suggestions in Discord in #artist-general. 

## Payout ⛽
Projects with multiple artists can use the additional payee address field to split project payments between multiple wallets for primary and secondary sales. When a project only has one artist, the additional payee field is commonly used to manage on-chain charitable donations. The charity’s wallet can be entered in the additional payee field. The percentage entered in the additional payee field will then be directly transferred to the charity as sales are made.

!!!danger Artists must propose changes to their payment addresses (and splits between primary/additional) for admin approval. Approval is granted before Mint #0!!!

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
