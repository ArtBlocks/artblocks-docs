---
order: 900
---
# Project Form Fields Guide

Below you'll find a guide to all form fields and buttons within testnet and mainnet.

## Project Page:

### Purchases Paused

The Purchases Paused button can be used to mint on both the artist staging platform and mainnet without unpausing your project. We suggest using this method to mint token #0 and mints on testnet to avoid any accidental early mints from other collectors.

### Edit Project

The Edit Project button will lead to the back-end of your shell where you will set up your project.

---

## Project:

### Project name*

This is the public name of your project.

### Artist name*

This is how your name will appear on Art Blocks. What you choose to enter here is up to your personal preference.

### Project website

This field is optional. The link entered in your project website field should lead to a place that exhibits more about your presented project or your background as an artist. This can link to a page that is specific to your project, your personal website, your instagram, your twitter, your github, or something else.

Make sure to enter a fully defined website link, including the `https://`

### Project description*

The description should summarize your practice specific to the project displayed — including inspiration, color palette influences, themes, and techniques. Your project description should include any interactions that your project has.

The description should open with a first line that encapsulates, as much as possible, what is most significant about the project.

The description should be between 80 and 140 words. The ideal description is ~120 words, though a tightly written 80-word description is preferable to a longer description that includes repetition and filler sentences.

### Project license*

Enter the copyright license here for your art (eg. NFT License 2.0, CC BY-NC 4.0, CC BY 4.0, etc)

Art Blocks recommends always selecting a license that aligns with your values as a creator.

---

## Token:

### Price per token in eth or ERC-20 equivalent*

If you are using a dutch auction sales mechanic, this should be your resting price as you are creating your shell. If the price is fixed, this will be your project’s fixed price.

In advance of your project launch, you will adjust this field to your dutch auction starting price and will submit price changes here every 5 minutes to manually adjust your project’s price.

### Drop mechanic description

Mention if your project will be using a Dutch Auction sales mechanic or will be fixed price. If Dutch Auction, list out your price tiers. Your sales mechanic description should also include your charity choice and donation amount. For any mints sold over 0.25eth, 25% is required to be donated to a charity of your choice.

### Currency symbol*

This will likely be ETH.

Alternatively, you may specify any ERC20-compliant token here. If you choose to do so, please give Sarah/the Art Blocks Team a heads up. If you are using a custom currency, enter the symbol for your currency here.

### Currency address

If you are accepting ETH as payment, this field should be blank. This field should only be set if you are accepting payment from your project in some non-ETH ERC20- compliant token.

### Maximum invocations*

This is your total project series size.

### Base uri*

If you are an artist, your project base uri field should be: https://api.artblocks.io/token/.

If you are Powered By Art Blocks (PBAB), see step 8 [here](../../powered-by-art-blocks-pbab-onboarding/pbab-101/adding-new-project-shells.md) for guidance.

---

## Script:

### Script type*

Select your script type and the version number of that dependency from the drop down menu provided.

### Aspect ratio (width / height)*

Your project’s outputs must be dimension agnostic, meaning it scales seamlessly to any window size. See more on this [here](readme.md#dimensionless). This field is used to set the aspect ratio for image renders, but does not have any impact on an output’s live view.

While you can control the aspect ratio, you will have no control over the dimensions of the browser someone else might be using.

Your aspect ratio should be a single number. This will be your token’s width divided by height. For example, if your tokens are square, your aspect ratio should be 1.

### Render delay*

If your piece takes a certain amount of time to fully render, you can type in the render delay to let the server know when to render your output’s thumbnails. This render time will be in milliseconds.

### Display static (toggle)

If red, then the project’s primary view will be dynamic, if blue the project’s primary view will be static.
These settings will be reflected on Art Blocks and also on OpenSea once the project is live.

If toggled blue, Art Blocks will display status as well which will improve performance if the piece is static and takes a long time to render.

### Project scripts*

Here you will upload your project’s script. Your features script should be separate from your project script.

Remember, tokenData.hash is a global variable in the environment this script will live in, so you do not need to define tokenData in your script, just expect your script will have access to it.

If your script is big, consider minifying it. There are no limits for total script length. That said, scripts that are larger than 10 kilobytes will need to be broken up into segments of 10kb. Segments can be added using the plus symbol (+) when uploading a script. Be aware that you will have to pay in transaction gas fees proportional to the size of script upload you are performing.

### Features

In order for filtering and rarity (% occurrence of different features) to be accessible via the Art Blocks website, the feature fields must be added in the artist interface UI on the Art Blocks website.

There are two types of feature fields: enum and number:

For enum fields, values should be outputted as strings in your features scripts. These should be entered as comma delimited strings with no quotation marks.

For number fields, the step size set in the feature fields is used for the step size of the slider in the filters. This step size is set in the feature fields UI, not in the script, and should be on a per field basis.

If there are only a few specific number values expected to be output, an artist might want to use an enum field and output the enumerated possible numeric values as strings (e.g. if the slider UI would not be the best way to navigate these features).

### Feature script

All code required for calculating your features (including any necessary helper functions) must be defined and implemented within the single top-level `calculateFeatures` function.

For many artists, the process for writing your features script will likely entail starting with your project script, copying it into the `calculateFeatures` interface/shell found [here](features.md#features-script-interface), and then trimming it down to remove all library (e.g. p5js) references and draw functionality and instead to build the relative key-value object map for your features.

---
## Minter

### MinterSuite 

The MinterSuite is an update to our broader smart-contract architecture at Art Blocks that allows artists to set specific minting contracts on a per-project basis.

The MinterSuite currently includes the following minter options, which will continue to expand over time:

• Dutch Auction - Linear Price Decrease
     Linear Dutch Auctions specify starting price, starting time, ending time, and ending price, and the price will linearly decrease over that time for        each block
• Dutch Auction - Exponential Price Decrease 
    Exponential Dutch Auctions are when the artist decides the half-life for each price drop
• Set Price - Custom ERC20
    Fixed price with a custom token
• Set Price - ETH
    Fixed price in ETH 

The MinterSuite includes support for a V1 series of the 4 initially introduced minters, to improve the experience for minting with smart contract wallets (e.g. Gnosis and Argent) and slightly reduce the gas-cost of minting in the process.


### How to set your project price

1. Determine your pricing. You have the option to choose between a set price in ETH, an automated linear dutch auction, an automated exponential dutch auction, or a set price in custom ERC20. The first step is to choose your desired selling option. The Art Blocks team can assist in determining this.
    a. Set price in ETH: Set price in ETH is a fixed price for your sale. 
    b. Automated linear dutch auction: For linear dutch auctions, artists will specify the starting price, ending price, starting time, and ending time of     the auction. The price will then gradually decrease each block over the total auction time. 
    c. Automated exponential dutch auction: For exponential dutch auctions, artists specify the starting price, ending price, and the half-life for price     drops. An easier way to determine this is to think of the total duration of the DA and then work backward to find the half-life at that total time. 
    As an example, let's say that an exponential dutch auction was starting at 1 ETH and lowering to 0.1 ETH over 30 minutes. In this case, the half-life     is 9 minutes meaning that over the course of every 9 minutes, the price would gradually be cut in half. So after 9 minutes, the DA will reach 0.5 and     after 18 minutes, the DA will reach 0.25. The price drops within those half-life steps will gradually lower every block. You can use this calculator       to find your auction’s half-life: https://www.calculator.net/half-life-calculator.html. Please note that results from that calculator will need to be     converted from minutes to seconds for Art Blocks. 
    d. Set price in custom ERC20: Set price in ERC20 is a fixed price for your sale with a custom token. Artists will specify the address for the custom       token. 
2. Input your pricing information. Go to the Minter tab within your shell and select the ‘minter for project’ drop-down menu. From that menu, select your desired MinterSuite option. [Please note that mint #0 will be created using the Set Price- ETH option. If your project will be sold via Dutch Auction, please set the price to your DA’s resting price for mint #0. After mint #0, you may then adjust the MinterSuite back to your desired option.] Once the price option has been selected from the drop-down menu, select Submit. After submitting, enter the required information for your MinterSuite choice below and submit.

---

## Payout:

### Additional payee address

Projects with multiple artists can use the additional payee address field to split project payments between multiple wallets. This option is limited to projects with two artists.

When a project only has one artist, the additional payee field is commonly used to manage on-chain charitable donations. The charity’s wallet can be entered in the additional payee field and the percentage entered in the additional payee percentage field will then be directly transferred to the charity as sales are made.

### Additional payee percentage: percentage allocated to additional payee address

This is the percentage that should be allocated to the additional payee address.

### Secondary market royalty

Secondary marketplaces can choose if they’d like to honor the secondary market royalty amount. OpenSea does not honor this field. On OpenSea, artists receive 5% of all secondary sales. Because of this, for consistency, we recommend setting your secondary market royalty to 5%.

The royalty field should be entered as a number and does not require a % symbol.

To learn more about royalty distributions, see [here](faqs.md#how-does-royalty-distribution-work).

---

## Danger:

### Artist address*

This will be the wallet address that you provide to us when setting up your shell. Should you need to transfer ownership, we cannot whitelist multiple wallets. Only the address entered in the artist address field will have access to the back-end of your project.

This is the address that will be used for payout.

### Unpause

When it is time for your project to go live, you will press the Unpause button in your mainnet shell. Once the transaction clears, your project will be live for minting.

---

## On Tokens

### Refresh Token Image

This button will queue your token thumbnail to be refreshed. The refresh is not instantaneous and may take time to fully process.

Rendering tokens does take computing power, of which we have a limited bandwidth. Please feel free to refresh tokens after making updates, but note that if our rendering pipeline starts clogging up with requests, we may have to consider rate-limiting refresh requests. In summary, use this button when testing out updates, but avoid spamming or things will get jammed up.

With this button, you can refresh per token. The AB Team has the power to refresh all thumbnails in a project at once and we are happy to do so for you.

### Details

The details page is specific to each token. On the details page, you will find the token’s features, a link to the transaction on Etherscan, and a link to the work on OpenSea.

### Image

The image button will generate a PNG of the token’s thumbnail.

### Live

As a note, the live generator view will give a bad request error until the project is public. Once a project is public, this link will function. While a project is private, live views can be viewed on the details section of the individual token.
