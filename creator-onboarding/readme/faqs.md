---
Order: 700
description: Frequently asked questions.
---

# FAQs

To suggest a question to be added, fill out this form: [Creator FAQs Suggestion Box](https://forms.gle/P3TJcZ8ydqFmMyiw9)

## Application

### When can I expect to hear back after I submit an application?

Once an application is submitted, it’s added to our pipeline for review. Depending on the volume of applications, it can take anywhere from a few weeks to a few months before you can expect to hear from us. The first conversation will focus on the status of your project, including reviewing test outputs.

We highly recommend you take advantage of this time to continue refining your script and to gather your supporting materials. This not only improves the project, but will accelerate the on-boarding process.

### What happens after I apply?

We'll reach out to check on the status of your project submission when we reach your application in the queue. You can share any updates with us, or let us know if you need a bit more time to finish uploading and iterating your script. After we have your final submission, it will be reviewed, and you will be notified whether or not your project is selected for an Art Blocks launch. If your project is selected, you'll move into the [Artist Onboarding Steps](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/artist-onboarding-steps/).

### What is the expected timeline for hearing back from Art Blocks throughout the application process?

Once your application has been reached in the queue, you can expect responses within 48 hours during weekdays. Please note that weekends are not working hours for Art Blocks. For communications sent over the weekend, please allow 72 hours for a response.

### How do I know the application period to send my first work?

For the time being, applications will remain open indefinitely. To learn more about the application process, visit [apply.artblocks.io](apply.artblocks.io).

### What is the process for submitting my first work?

You may apply using [this application form](artblocks.io/apply). We expect that artists have a creative history and the ability to provide an original generative script.

## Artist Pipeline 

### What are the steps in the process and how do I know when I've completed them?

Please see [Artist Onboarding Steps](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/artist-onboarding-steps/) for a more detailed overview of the onboarding process.

### Approximately how long will each step of the process take?

Once the artist onboarding process begins, it will take approximately 1-2 months to upload your project, finalize it on testnet, submit it for curation review, finalize it on mainnet, schedule a launch date, and finally release the project. The length of each step differs and depends somewhat on how quickly you, the artist, finalize your scripts. Please see our artist onboarding flow for more information about the timeline of each step.

### Who can I reach out to if I have questions?

For questions related to your application, please post your inquiry in #artist-application-support. You may also use the #help channel 

## Curation Review 

### What are the general standards for achieving curation status? 

The Curated Collection is a group of projects that pushes the boundaries of Generative Art. A project in the Curated Collection covers new territory using code that employs inventive, never-before-seen techniques to support an original intention and concept. Board members look for collections that evoke emotional, intellectual, and conceptual qualities through aesthetics while sustaining the viewer’s interest.

### Are rarities judged as a metric for curation?

Rarities aren't included as a metric for determining curation status. However, the overall variety of a collection is important so that the project contains diversity over the course of a large number of mints.

### Will I receive feedback from the curation board on my submissions?

Feedback from the Curation Board will be provided. The goal of this feedback will be to highlight observations that our Curation Board made about your current project upon their review.

### Who is on the curation board?

Art Blocks has invited individuals to our Curation Board based on their expertise, passion for the evolution and growth of on-chain generative art, and their industry leadership.

You can read more about the Curation Board [here](https://info.artblocks.io/spectrum/meet-the-art-blocks-curation-board).

## Technical Requirements

### Are all browsers supported for Art Blocks drops? Is mobile supported?

All modern browsers are supported (including mobile), though you may run into issues using Internet Explorer. We recommend using Browserstack https://www.browserstack.com/ to test across devices.

### Do I need to know Solidity (to write my own smart contract)?

No. Art Blocks handles all of that for you. All you need to create is the artwork.

### Can I load external assets into my project (textures, audio, etc)?

Not at this time. Currently, everything must be included in the script file. For small and critical assets, you may be able to use `base-64` encoding to encode the asset into your script, but that will count as data to be stored.

### Can I use text? What fonts can I use?

You can use text in your project! Font choice is technically at your discretion, but you're encouraged to use the core web fonts to ensure universal support and maintain the piece's integrity over the longer term. (`serif,` `sans-serif,` `monospace`, and less commonly, `cursive` and `fantasy.`)

### What are the minimum hardware requirements? What type of graphics card do I need?

Any computer with an internet connection will work! No special graphics cards are required.

## Staging 

### Is it possible to see my project without being connected to my wallet? So I can test it across different devices and browsers without connecting?

No, this is not currently possible. You'll need to be signed in with your wallet to access your project. You can however view live view links without being connected to a wallet. To view a live view link while your shell is private, add `?render=true/` to the end of the URL.

### What is the MinterSuite, and how does it work? 

The MinterSuite allows artists to set specific minting contracts on a per-project basis. The MinterSuite currently includes the following minter options, which will continue to be expanded over time: 

**Set Price - ETH** is used for fixed price releases.

**Automated Exponential Dutch Auction**: For exponential Dutch auctions, artists specify the starting price, ending price, and the half-life for price drops.

**Automated Linear Dutch Auction:** For linear Dutch auctions, artists will specify the starting price, ending price, starting time, and ending time of the auction. The price will then gradually decrease each block over the total auction time.

**Set price in custom ERC20:** Set price in ERC20 is a fixed price for your sale with a custom token. Artists will specify the address for the custom token sale. 

**Set Price - ETH, Allowlisted Users Only (V1)** these are addresses that are allowed to mint as many times as they want until they reach the mint limit (artists sets mint/wallet)

To find out how to set your project price using the MinterSuite visit [this page](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/project-form-fields-guide/#minter). 

## Uploading Your Script 

### How much money / ETH do I need to upload my project?

The cost depends on the complexity of your project and how many lines of code it requires. See [here](readme.md#cost) for more specific information about how to budget for a drop.

### My project is uploaded and ready to go. How do I mint my first output?

You can use the “Purchases Paused” button to mint both on the artist staging platform and mainnet _**without**_ unpausing your project. We suggest using this method to mint Token #0 to avoid any accidental early mints.

### Are there limits on script length?

If your script is big, consider minifying it. There are no limits to the total script length. That said, scripts that are larger than 24 kilobytes will need to be broken up into segments of 24kb. Segments can be added using the plus symbol (+) when uploading a script. Be aware that you will have to pay transaction gas fees proportional to the size of the script upload.

###  Does the size include the library that I'm using?

No, the library you use is not stored on-chain with your project. A script tag linking to a CDN hosting the library you choose will be injected into the window scope when the project runs.

## Preparing for your drop 

### What information will I need to provide about my project?

If your project is selected for a drop on Art Blocks, you'll need to have the following information ready. This is typically collected near the end of the process, so you'll have time to make these decisions as you're onboarding.

```
Would you like your Goerli testnet project made public? YES/NO

[Curated/Presents]
Project name:
Artist name:
Project Link: https://www.artblocks.io/project/[#]
Project Conversations: #block-talk or #\[artist-name]
Start Date/Time: To be determined with the Art Blocks team
Total Mints:
Drop Mechanic (fixed price/Dutch auction):
Mint Price (start price and resting price if Dutch auction):
Charity Info (if applicable):
```

### Can I share information about my drop on social media before it's announced?

Once you finalize a drop date with the Art Blocks team, you're welcome to share and promote your drop on all social media! We have created a [Marketing  101](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/marketing101/#marketing-101) document to support your efforts in the lead-up to your drop. 

### When will I know when my drop is scheduled? When will the drop be announced?

Once your application is approved, it takes approximately 6-8 weeks to reach a launch date for your project. You'll work closely with our team to schedule a drop date, which typically will be about 2 weeks after your project is finalized on mainnet. Every Friday, our team announces the following week's projects in the Discord channel, #upcoming-projects.


### Can I mint pieces of my own artwork? How many?

All artists on Art Blocks will mint the first piece (mint #0) of the collection for themselves. If you collaborated with other artists, you can each mint one of the first outputs before the project goes live.

If you're dropping in the Presents category and you'd like to mint more pieces of the collection (for gifts or giveaways), let us know in your artist DM. If you’d like to mint more than just Mint #0, wee ask that you clearly communicate why you're minting more than one to the community.

## Price Mechanics 

### How should I price my artwork?

Once you near the finalization of your project, you'll be in close dialogue with our team about how to price your work. We have a [Project Pricing Model](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/project-pricing-model/) that guides the decision on the pricing of Art Blocks collections. 

### How is project revenue shared?

Art Blocks is allotted 10% of the total primary sales and 2.5% of secondary sales. Artists can donate a percentage of sales to a charity of their choice to be distributed on primary and/or secondary sales. Artists will also receive 5% of secondary sales in perpetuity. 

### What percent of secondary royalty sales do artists receive?

On OpenSea, the most popular secondary marketplace, artists receive 5% of all secondary sales, and Art Blocks receives 2.5% of all secondary sales.

On other platforms, artists can set their own secondary percentage on their project for other markets that may recognize that field. For consistency, we recommend setting your default secondary market royalty to 5%.

### How does royalty distribution work?

Royalty distribution varies based on the secondary marketplace. Most secondary marketplaces (Rarible,Archipelago, Looksrare etc.) will read your royalties from your contract (the secondary market royalty field) and will send the ETH accordingly directly to the wallet associated with the project.

OpenSea is the exception to this. OpenSea will collect royalties on the secondary sales directly (5%). These royalties are then transferred to Art Blocks and Art Blocks will then manually transfer those royalties to each artist. Royalty distributions will be announced in our artist channel.

### How can I customize revenue splits?
Setting up revenue splits can be done through the [Payout](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/project-form-fields-guide/#payout) fields in your project form. You can use the additional payee field within the form directly to send a portion of the revenue to that account. Many artists use this to make a charitable donation. To split revenue with more than one account, we recommend using [0xSplits](https://www.0xsplits.xyz/). Instructions on how to create a Split can be found [here](https://www.youtube.com/watch?v=P_uqQJghNAo). Once your Split is created, paste the address into the additional payee field.

### Do you have access to historical data of other Art Blocks sales? 

There are a few helpful tools for this:
 1. https://artacle.io/ 

This resource has most Art Blocks projects and will show the distribution of sales for Dutch Auctions.

2. https://rarity.guide/ 

This focuses on the rarity of mints per project, the time between mint #2, and the rate of sales.

## Charitable Giving 

### What is Art Blocks' commitment to charitable giving?

To maintain our commitment to charitable giving, we ask artists to consider donating 25% of sales above the resting price via Dutch auction to a charity of their choice. If you elect to participate in this way, please determine your chosen charity, and confirm its eligibility, before mint #0. To whom and how you donate is entirely up to you. Art Blocks does not require you to donate any proceeds in order to engage with our platform. If you do elect to donate to a charity, it is advisable to consider whether the charity which you choose to support qualifies under United States tax law to receive tax-deductible donations. If your project designates only one primary wallet, you may use the additional payee field to manage on-chain donations. All revenue may also be routed to a single wallet and donated after your drop. We encourage you to consult with a tax professional to understand any potential tax implications of your planned giving, as these can be widely variable.

### Where can I find a list of charities that accept crypto donations?

To find a list of charities, you can ask for advice in #artist-general and check the pinned messages for a charity guide. 

If the charity you’d like to donate to is not set up to receive crypto donations, we recommend checking out endaoment.org or CryptoForCharity.io. They both enable on-chain donations to any US-based 501c(3). Endaoment uses a Donor Advised Fund (DAF) model and has a 1.5% fee; CryptoForCharity sends the gifts on as they're made and is zero fee. This method can also be done fully on-chain, so the donations go directly to the charity, as opposed to going through the project’s designated primary wallet. Please note: different methods of distribution can have different tax implications, and Art Blocks advises every artist to consult with a tax professional when making these plans.. 

### How can I donate to charity?

Here are a few donation options:

**1) On-chain donations through Endaoment.org**

Endaoment is a 501c(3) organization that accepts crypto and distributes donations to any qualified US-based 501c(3) charity. Donations through Endaoment are set at the contract level and automatically routed at the time of payment.
To use Endaoment, go to Endaoment.org and create a fund. Then, enter ` 0x9D5025B327E6B863E5050141C987d988c07fd8B` or  `ndao.eth` in the additional payee field. Once you’ve created the fund, contact us in your [M_] artist DM with your fund’s URL and project number. Once your project launches and the money is in your Endaoment Fund, you can send donations to any qualified charity in the United States. Many artists prefer this route so they can support multiple charities with donations, rather than just one charity with a single donation. *Please note that Endaoment charges 1.5% to receive, convert, and send money to a charity.

You can also find a tutorial of how to use Endaoment [here](https://www.loom.com/share/822350f1a1c84f25b253cc9e4d2cee38).

**2) Make a zero-fee on-chain donation with CryptoforCharity.io**

CryptoForCharity is a zero-fee platform that enables donations in crypto assets directly to charity. Any qualified US-based 501c(3) charity  and several cause funds focused on a specific issue.

Donations through CryptoForCharity are set at the contract level and automatically routed at the time of payment.

Generating a charity or cause fund wallet is straightforward -- fill out the form [here](https://www.cryptoforcharity.io/nft-creators). You can also contact SimonSays#0670 in the Art Blocks discord for help.

For a bit more on how this functions, [CryptoForCharity put together this tax guidance for NFT creators](https://www.cryptoforcharity.io/nft-creators).  

**3) Create a second wallet**

If you’d like to create an additional wallet separate from the primary wallet designated for the project, you can enter that wallet's address in the “Additional Payee” field to collect the funds you intend to donate.

**4) Receive funds in your primary wallet**

If you’d like to receive all funds from your project’s sale in your primary wallet, but still intend to participate in charitable giving, we recommend you communicate the total donations with Art Blocks and the community. Please be aware that each of the different methods of distributing funds can have its own tax implications, and Art Blocks recommends you consult a tax professional when making these plans. 

### How do I adjust charitable giving information from the additional payee field mid-Dutch auction?

If charity information is entered as an additional payee field and you would like to remove this information prior to decreasing your tier below resting price, please adjust the additional payee field to either 0x0000000000000000000000000000000000000000 or to the project’s primary wallet address and adjust the additional payee percentage to 0% before submitting the next price tier. These fields cannot be blank once the Dutch auction has begun.

## Security 

### Where can I learn more about best practices for security, including hardware wallets?

We recommend that all users have a hardware wallet that they use to interact with MetaMask.

You can learn more about security in the NFT space [here](https://medium.com/the-link-art-blocks/how-to-secure-your-collection-3dca5c073aef) (how to keep your collection safe) and [here](https://medium.com/the-link-art-blocks/avoiding-scams-and-staying-safe-9a6808a4146e) (how to avoid scams).

You can also check out our [After Dinner Mints episode](https://www.youtube.com/watch?v=u8MK99grAfI) dedicated to security!

## Artist Community 

### Is there a place I can connect with other artists and chat?

All artists are added to the artist-exclusive #artist-general channel in Discord, where you can interact with other Art Blocks artists, share projects, and ask questions. We encourage artists to participate in our Discord community. In addition, Art Blocks hosts a weekly [Office Hours](https://calendar.google.com/calendar/u/1?cid=Y192a2RxdWluZ3ZsM2EyMmJudWxxZnFkb2sxOEBncm91cC5jYWxlbmRhci5nb29nbGUuY29t). This dedicated time is the place for artists to chat synchronously, meet the Art Blocks team, participate in artist development-focused programming, and group critiques. If your project has been chosen for an Art Blocks Curated release, we will establish a dedicated artist’s  Discord channel for you  to centralize discussions of that project. For all artists releasing on Art Blocks, , the #block-talk channel is a great place to interact with fellow artists, collectors, and community members. 

## Post-Drop 

### How long do I need to wait before releasing a project through Art Blocks again?

When an artist’s project is 100% minted (i.e. “complete”), the artist is eligible to submit a new project for screening. Please note: there is a six month “cool-off” period after a Curated project is complete before the artist may submit another project for consideration as Curated.. 

### Will I have access to my testnet shell after I release my project?

Yes. Please note, as of Aug 2, 2022, Art Blocks switched testing networks from Ropsten to Goerli.

If you previously had a testnet shell on the Ropsten network, you may still access your project shell using https://ropsten-artist-staging.artblocks.io/ as a read-only set of data. If you are a returning artist, please write in your artist DM, or in #artist-general. 

### What is the process upon returning to Art Blocks as a non-Curated artist?

After your project is completed, you will be eligible to submit a new project for screening consideration. You will continue to have access to your testnet shell. New projects can be submitted for review either via a working prototype or via your existing testnet shell, to which you will continue to have access. To submit a new project for screening by sending a message to your Artist DM. 

The first screening determines if a work is accepted onto the platform. A committee made up of Art Blocks' staff and generative art experts conducts this screening. This review focuses on overall aesthetics, mint variety, and the degree to which a project explores new territory technically, visually, and conceptually. Returning artists are still subject to the highly-selective screening process.

If the work is accepted to be released on Art Blocks you will then move through the same onboarding process as your previous project, which is also outlined [here](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/artist-onboarding-steps/#5-feedback-check).

