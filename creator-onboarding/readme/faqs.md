---
Order: 700
description: Frequently asked questions.
---

# FAQs

To suggest a question to be added, fill out this form: [Creator FAQs Suggestion Box](https://forms.gle/P3TJcZ8ydqFmMyiw9)

## Application

### How can a generative artist be published in Art Blocks?

Art Blocks has an application form that generative artists can submit. Please note that we are becoming increasingly selective, only accepting around 2% of projects submitted for release.

You can find out an application here: [artblocks.io/apply](https://www.artblocks.io/apply)

You will receive a project shell on our staging site when you apply. This project shell is where you will upload your project to Art Blocks for review. Only the wallet address connected to Art Blocks will have access to the project shell when applying. The shell creation ensures that all projects are compatible with Art Blocks and reviewed using a standard format.


### When can I expect to hear back after I submit an application?

When you're ready to proceed to our screening stage, please email apply@artblocks.io with a link to your staging shell. 
Before the screening, ensure the work has a project description that explains the work's technical, aesthetic, and conceptual approaches. Prototypes should have 40-50 mints, as well as feature traits. Also include an artist profile and links to any ancillary material about the work on the project page. All prototypes should be completely finished before review. The team will let you know when the work will be screened and give you a timeline for the acceptance decision. 

### Are we notified of the result (accepted/rejected) or only if it is accepted?

After you notify the team that you are ready for review by emailing apply@artblocks.io, the team will let you know when the work will be screened and give you a timeline for the acceptance decision. 

### If I change my mind about the collection I am trying to release, can I just change it in my current project id, or should I re-apply?

Please reuse the shell that was created upon application if you’d like to submit a new project, and this process is applied to artists who were rejected and would like to re-submit a prototype for review. Upload your new script and refresh the thumbnails to update your staging shell. 

### What happens after I apply?

Once you apply, you will have access to a staging shell on testnet. There, you can upload your generative script and mint test outputs. Prototypes should have 40-50 mints, a project description, and feature traits. Also include an artist profile and links to any ancillary material about the work on the project page. When you're ready to proceed to our screening stage, please email apply@artblocks.io with a link to your staging shell. All prototypes should be completely finished before review. The Art Blocks team will give you a timeline as to when the project will be reviewed and when you will be  notified whether or not your project is selected for an Art Blocks launch. Please note, we are becoming increasingly selective, only accepting 2% of projects submitted for release. Take your time in the artistic process to ensure you are bringing forth your best work. 

### I cannot fill out the application form on Typeform. 

Please note that we have moved our application to artblocks.io/apply. You will receive a project shell on our staging site when you apply. This project shell is where you will upload your project to Art Blocks for review. Only the wallet address connected to Art Blocks will have access to the project shell when applying. The shell creation ensures that all projects are compatible with Art Blocks and reviewed using a standard format.

### How do I know the application period to send my first work?

Applications will remain open indefinitely. To learn more about the application process, visit [artblocks.io/apply](artblocks.io/apply). 

### What is the process for submitting my first work?

You may apply using [this application form](artblocks.io/apply). 

### I received a link to upload my prototype, but it's not working; what should I do? 

Clear your cache and ensure you are connected to the wallet you applied with and using the Goerli test network. 

### At the time of submission, I did not put a project preview. If I do it now, does it restart the application process to zero? Can it help in the process?

Applications are logged in chronological order in our database. You will let us know that your prototype is ready to be reviewed for release by emailing apply@artblocks.io. Before the screening, ensure the work has a project description that explains the work's technical, aesthetic, and conceptual approaches. Prototypes should have 40-50 mints, a project description, and feature traits. Also include an artist profile and links to any ancillary material about the work on the project page. All prototypes should be completely finished before review. 

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

### The documentation states that only one external library can be used, and then there is a list of some libraries. I’m unsure if this is the list of libraries allowed to use or only examples of popular libraries. Can I, for example, use a game engine library that is not on that list? 

Everything on the limited dependencies list in our Creator Documentation is compatible with the platform. See here: https://docs.artblocks.io/creator-docs/creator-onboarding/readme/#limited-dependencies

### I have opened my shell on the staging site but cannot upload sample outputs of my prototype. 

You must first upload your prototype script and then mint test outputs. Learn how to mint without unpausing your project here: https://docs.artblocks.io/creator-docs/creator-onboarding/testnet-checklist/#test-minting

### Is it possible to create a project on the site without a library code? Is it possible to do a project based on ipfs, or should everything be generated exclusively on Art Blocks? 

All Art Blocks work is completely on-chain. Artists must upload their technically-compatible project scripts to their staging shell to produce a collection. All projects must use the limited dependencies outlined in our Creator Documentation: https://docs.artblocks.io/creator-docs/creator-onboarding/readme/#limited-dependencies

### My script works and is shown in "Explore Possibilities," but my test mints are not showing. The console is showing many NextJs script errors. Any suggestions? Could it be my script's fault?

Your script must be the same version of the [limited dependencies](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/#limited-dependencies) accepted by the platform. 

Consider using this starter template, which gives you an environment similar to Art Blocks: https://github.com/ArtBlocks/artblocks-starter-template 

### Where do I add my public files in the staging environment (html, CSS)? 

You only need to submit the prototype script, then you can choose a library in the `script` tab of the `edit project` which will add the container(canvas) and the script import.

### There is a difference between my thumbnails and the live views. 

Randomness becomes deterministic when it's seeded, which is what's happening with the Art Blocks token data and suggested Random class. Once initialized, all calls to the random_dec method must remain consistent.  Resolving anything random before starting to draw is handy in that regard, plus you'll also need to provide that code for the calculateFeatures function.

If you're getting inconsistent outputs, the first thing would be to ensure there's no any forgotten Math.random() in your code and that your token data looks okay.

### My artwork depends on some deterministic Random function calls, and features depend on it. In the staging environment, the features script is completely separated from the artwork script. How can I calculate the features? The only solution I can see is to rewrite the random calls in the feature script in the same order they are called in the artwork script. Any different, simpler, and safer. approach to suggest me?

You will rewrite the random calls in the feature script in the same order they are called in the artwork script. More info here: https://docs.artblocks.io/creator-docs/creator-onboarding/readme/features/

### I set up the features, types, and options in my staging shell, and copied my original code into the `Calculate Features` section, removed all the p5.js drawing, then set it up to build key-value pairs. Right now, I have the key-value pairs being assigned to an object called "features." How do I get the script to return the right object? The code isn't giving me any errors, but no features appear when I look at the mints. 

You should have the function return the dictionary with the features iirc, using the syntax `return {object name}`. If the problem still occurs, clear your cache. There may also be an authentication issue, so log out and log back into your wallet. 

### Can I visually verify my code is working properly through the Art Blocks staging platform?

If you can mint test outputs successfully, your script will likely be compatible with the platform. Check out our technical documentation here: https://docs.artblocks.io/creator-docs/creator-onboarding/readme/#documentation

### Where is the mint button? Do we have to set a price? 

Learn how to mint without unpausing your project here: https://docs.artblocks.io/creator-docs/creator-onboarding/testnet-checklist/#test-minting

## Artist Pipeline 

### What are the steps in the process and how do I know when I've completed them?

Please see [Artist Onboarding Steps](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/artist-onboarding-steps/) for a more detailed overview of the onboarding process.

### Approximately how long will each step of the process take?

Once a project is accepted for release, it will take approximately 1-2 months to finalize your project on testnet, submit it for curation review, upload the script on mainnet, schedule a launch date, and finally release the project. The length of each step differs and depends somewhat on how quickly you, the artist, finalize your scripts. Please see our [Artist Onboarding Steps](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/artist-onboarding-steps/) for more information about the timeline of each step.

### Who can I reach out to if I have questions?

For questions related to your application, please post your inquiry in #artist-applications. You may also use the #help channel 

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

You can use text in your project! Font choice is technically at your discretion, but you're encouraged to embed them in your scripts directly or use the core web fonts to ensure universal support and maintain the piece's integrity over the longer term. (`serif,` `sans-serif,` `monospace`, and less commonly, `cursive` and `fantasy.`)

### What are the minimum hardware requirements? What type of graphics card do I need?

Any computer with an internet connection will work! No special graphics cards are required.

## Uploading Your Script to Mainnet

### How much money / ETH do I need to upload my project?

The cost depends on the complexity of your project and how many lines of code it requires. See [here](readme.md#cost) for more specific information about how to budget for a drop.

### My project is uploaded and ready to go. How do I mint my first output?

You can use the “Purchases Paused” button to mint both on the artist staging platform and mainnet _**without**_ unpausing your project. We suggest using this method to mint Token #0 to avoid any accidental early mints.

### Are there limits on script length?

If your script is big, consider minifying it. There are no limits to the total script length. That said, scripts that are larger than 24 kilobytes will need to be broken up into segments of 24kb. Segments can be added using the "add script segment" button when uploading a script. Be aware that you will have to pay transaction gas fees proportional to the size of the script upload.

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

As an artist, you should be aware of recent changes in royalty rate determination at OpenSea and Blur, which have resulted in a range of royalty payment percentages (from 0% to 5%). Due to this change, we've had to adjust our royalty payout calculations.

We've chosen to uphold the same royalty split ratio between our Artists and Art Blocks (2/3 for the Artist and 1/3 for Art Blocks). Art Blocks handles the distribution of royalty payments received from marketplaces that do not offer direct splits through the Royalty Registry, following an internal review of secondary sales transactions.

If you have any questions regarding this updated split methodology or information regarding royalty payouts, please post in #artist-general on Discord. 

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


**1)** **On-chain donations through Endaoment.org**

Endaoment is a 501(c)(3) organization that accepts crypto and distributes donations to any US-based 501(c)(3) charity in good standing with the IRS. Donations through Endaoment are set at the contract level and automatically routed at the time of payment without touching your wallet (potentially avoiding tax liability/deductibility).

To use Endaoment, go to [Endaoment.org](https://endaoment.org), connect your wallet and create a fund. Then, enter your fund's contract address (shown on your newly created fund page) in the additional payee field. If using the additional payee field for donations, this field can be cleared before lowering to resting price. Many artists prefer this route so they can support multiple charities with smaller donations rather than a single charity with one large donation, but you can also set up organization as additional payee directly. In this case, go to [Endaoment.org](https://endaoment.org/explore), use their search bar to locate the org in question, and copy the contract address directly from the organization's profile page to the payee field (you can do this for multiple charities if desired). If the organization(s) shows as 'Not Deployed', simply click 'Deploy' to create a smart contract for that nonprofit. When that process completes, a contract address will populate on the organization's profile page. After the mint concludes, contact Dan (Druid#4611 on Discord) with your fund’s URL or smart contract address. Endaoment will then process contributed ETH into USDC, allowing you to send donations in any amount to any charity in the US using their UI. Please note - Endaoment charges 1.5% to receive, convert, and distribute money to nonprofits.

You can also find a tutorial of how to use Endaoment [here](https://www.loom.com/share/822350f1a1c84f25b253cc9e4d2cee38), can find direct support in their Discord server [here](https://discord.gg/endaoment) by creating a ticket in the #🙋｜get․help channel, and can read up on their documentation [here](https://docs.endaoment.org).

**2)** **Make a zero-fee on-chain donation with CryptoforCharity.io**

CryptoForCharity is a zero-fee platform enabling donations in crypto assets directly to charity. You can support any US-based 501(c)(3) charity in good standing with the IRS, or donate to any of several cause funds focused on a specific issue.

Donations through CryptoForCharity are set at the contract level and automatically routed at the time of payment without touching your wallet (and potentially avoiding tax liability or the need to account for and deduct the income/donation). Donated funds can also be held for a short time following your drop, if you'd prefer to designate the charity or cause fund you wish to support after the fact, but they cannot be held indefinitely.

Generating a charity or cause fund wallet is straightforward -- simply fill out the form [here](https://www.cryptoforcharity.io/nft-creators). You can also reach out directly to SimonSays#0670 in the AB discord for help.

For a bit more on how it's set up under the hood, [CryptoForCharity put together this tax guidance for NFT creators](https://www.cryptoforcharity.io/nft-creators).  

**3)** **Create a second wallet**

If you’d like to create a second wallet separate from your personal wallet, you can enter the wallet's address in the additional payee field to collect the total donation amount you intend to donate. If using the additional payee field for donations, this field can be cleared before lowering to resting price.

**4)** **Receive funds in your primary wallet**

If you’d like to receive all funds from your project’s sale in your primary wallet, that’s fine, but please communicate the total donations with Art Blocks and the community. Please be aware that receiving money in your personal wallet may incur tax obligations and reduce the total donation amount.

## How do I remove charitable giving information from the additional payee field mid-Dutch Auction?

If charity information is entered as an additional payee field and you would like to remove this information prior to decreasing your tier below 0.25 ETH, please adjust the additional payee field to either 0x0000000000000000000000000000000000000000 or to your own wallet address and adjust the additional payee percentage to 0% before submitting the next price tier. These fields cannot be blank once the dutch auction has begun.

## What has Art Blocks donated to charity in the past?

To learn more about Art Blocks commitment to charitable giving, see our [Charity on Chain: 2021 Wrap-Up](https://medium.com/the-link-art-blocks/charity-on-chain-2021-wrap-up-c69782fa7f4a).

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

