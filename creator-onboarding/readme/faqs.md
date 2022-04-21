---
order: 800
description: Frequently asked questions.
---
# FAQs

To suggest a question to be added, fill out this form: [Creator FAQs Suggestion Box](https://forms.gle/P3TJcZ8ydqFmMyiw9)

---

## When can I expect to hear back after I submit an application?

Once an application is submitted, it’s added to our pipeline for review. Depending on congestion, it can take anywhere from a few weeks to a few months before we reach out to get the process started. The first conversation is focused on the status of your project and seeing what you’ve been working on.

We highly recommend you take advantage of this time and continue refining your script. This not only improves the project but speeds up the onboarding process once conversations start.

---

## What happens after I apply?

After an application period ends, our creative team will begin the process of reviewing applications in the order they were received. We'll reach out to check on the status of your project prototype when we reach your application in the queue. You can share any updates with us, or let us know if you need a bit more time to finalize a prototype. After we have your final submission, you'll hear back from us whether or not your project is selected for an Art Blocks launch. If your project is selected, you'll move into the Artist Onboarding process.

---

## What are the steps in the process and how do I know when I've completed them?

Please see our Artist Onboarding Steps page for a more detailed overview of the onboarding process.

---

## Approximately how long will each step of the process take?

Once the artist onboarding process begins, it will take approximately 4-6 weeks to upload your project, finalize it on testnet, submit it for curation review, finalize it on mainnet, schedule a launch date, and finally release the project. The length of each step differs and depends somewhat on how quickly you, the artist, finalize your scripts. Please see our artist onboarding flow for more information about the timeline of each step.

---

## What is the expected timeline for hearing back from Art Blocks throughout the application process?

Once your application has been reached in the queue, communication will move quickly. During weekdays, you can expect responses within 24 hours. Please note that weekends are not working hours for Art Blocks. For communications sent over the weekend, please allow 72 hours for a response.

---

## Who can I reach out to if I have questions?

Sarah ([!badge Discord: sross#6444]), our Artist Liaison will be your primary point of contact, along with Jeff Davis ([!badge Discord: jeffgdavis#0102]), our CCO. You can reach them on Discord or send them an email.

---

## What are the general standards for achieving curation status? What are the criteria that differentiate curated and factory?

For each project, our curation board looks at overall aesthetics, variety in mints, and the degree to which a project explores new territory technically, visually, and conceptually.

It's important to note that curation status is not strictly a designation of quality. Instead, the curated collection indicates a substantial addition to Art Blocks' narrative within generative art.

For example, a project may be a technical, visual, and conceptual masterpiece, but if the idea has previously been explored in the curated collection, it may not substantially add to the broader narrative.

---

## Why are rarities judged as a metric for curation?

Rarities aren't included as a metric for determining curation status. However, overall variety of a collection is important so that the project continues to be exciting over the course of a large number of mints.

---

## Will I receive feedback from the curation board on my submissions?

If requested, feedback from the Curation Board can be provided. The goal of this feedback will be to highlight observations that our Curation Board made about your current project upon their review

---

## Who is on the curation board?

Our Curation Board is made up of a diverse group of artists and people in the art space. You can read more about the Curation Board on our Medium page: https://medium.com/the-link-art-blocks

---

## Are all browsers supported for AB drops? Is mobile supported?

All modern browsers are supported (including mobile), though you may run into issues if using internet explorer.

---

## Do I need to know Solidity (to write my own smart contracts)?

No. Art Blocks handles all of that for you. All you need to do is the artwork.

---

## Does the size include the library that I'm using?

No, the library you use is not stored on-chain with your project. A script tag linking to a CDN hosting the library you choose will be injected into the window scope when the project runs.

---

## Are there limits on script length?

If your script is big, consider minifying it. There are no limits for total script length. That said, scripts that are larger than 10 kilibytes will need to be broken up into segments of 10kb. Segments can be added using the plus symbol (+) when uploading a script. Be aware that you will have to pay in transaction gas fees proportional to the size of script upload you are performing.

---

## Can I load external assets into my project (textures, audio, etc)?

Not yet. Some ideas are being worked on that will allow external assets to get pulled in, but currently everything must be included in the script file. For small and critical assets, you may be able to use `base-64` encoding to encode the asset into your script, but that will count as data to be stored.

---

## Can I use text? What fonts can I use?

You can use text in your project! Font choice is technically at your discretion but you're encouraged to use the core web fonts to ensure universal support and maintain the integrity of the piece over the longer term. (`serif`, `sans-serif`, `monospace` and less commonly `cursive` and `fantasy`)

---

## What are the minimum hardware requirements? What type of graphics card do I need?

Any computer with an internet connection will work! No special graphics cards required.

---

## Is it possible to see my project without being connected to my wallet? So I can test it across different devices and browsers without having to connect?

No, this is not currently possible. You'll need to be signed in with your wallet to access your project.

---

## How much money / ETH do I need to upload my project?

The cost depends on the complexity of your project and how many lines of code it requires. See [here](readme.md#cost) for more specific information about how to budget for a drop.

---

## What information will I need to provide about my project?

If your project is selected for a drop on Art Blocks, you'll need to have the following information ready. This is typically collected near the end of the process, so you'll have time to make these decisions as you're onboarding.

```
Would you like your Ropsten testnet project made public? Y/N

[Curated/Playground/Factory]
Project name:
Artist name:
Project Link: https://www.artblocks.io/project/[#]
Project Conversations: #factory-projects or #\[artist-name]
Start Date/Time: TBD with the AB team
Total Mints:
Drop Mechanic:
Mint Price:
Pricing Tiers (if DA):
Charity Info (for any mints sold over 0.25eth, 25% is required to be donated to charity of your choice):
```

---

## My project is uploaded and ready to go. How do I mint my first output?

You can use the Purchases Paused button to mint both on the artist staging platform and mainnet _**without**_ unpausing your project. We suggest using this method to mint Token #0 to avoid any accidental early mints from other collectors

---

## Can I share information about my drop on social media before it's announced?

Once you finalize a drop date with the Art Blocks team, you're welcome to share and promote your drop on all social media!

---

## How should I price my artwork?

Once you near finalization of your project, you'll be in close dialogue with our team about how to price your work. Ultimately, we will defer to the artist to decide how to price a work, but can offer recommendations, advice, and context based on the market conditions at the time of your drop.

---

## How should I set up a dutch auction? How many price decrements should there be? What should I set for my floor price?

The structure and price levels of a dutch auction are largely up to the artist, but the Art Blocks team is happy to work with you directly to offer advice for price structuring based on market observations.

---

## I used a custom currency for my project. How do I get back to ETH?

To switch back to ETH, change the currency symbol to ETH and the contract address to 0x0000...

---

## What percent of project profits does Art Blocks take?

Art Blocks takes 10% of the total primary sales and 2.5% of secondary sales.

---

## What percent of secondary royalty sales do artists receive?

On OpenSea, the most popular secondary marketplace, artists receive 5% of all secondary sales and Art Blocks receives 2.5% of all secondary sales.

On other platforms, artists can set their own secondary percentage on their project for other markets that may recognize that field. For consistency, we recommend setting your secondary market royalty to 5%.

---

## How does royalty distribution work?

Royalty distribution varies based on the secondary marketplace. Most secondary marketplaces (Rarible, etc.) will read your royalties from your contract (the secondary market royalty field) and will send the ETH accordingly directly to you.

OpenSea is the exception to this. OpenSea will collect royalties on the secondary sales directly (5%). These royalties are then transferred to Art Blocks and Art Blocks will then manually transfer those royalties to each artist. Royalty distributions will be announced in our artist channel.

---

## What is Art Blocks commitment to charitable giving?

To maintain our commitment to charitable giving, we ask artists to consider donating 25% of profits above resting price via Dutch auction to an eligible charity of their choice. If this applies to your works, please determine your eligible charity of choice before mint #0. To whom and how you donate is up to you but you should consider whether the charity or the cause you are donating to qualifies under United States tax laws as a charity/cause that is qualified to receive tax-deductible donations. If you are a single artist, you may use the additional payee field to manage on-chain donations. All revenue may also be routed to a single wallet and donated after your drop. We highly recommend consulting with a tax professional to understand your local tax liability, especially if you plan to personally receive all funds before donating.

---

## Where can I find a list of charities that accept crypto donations?

To find a list of charities, you can ask for advice in #artist-general and check the pinned messages for a charity guide.

If the charity you’d like to donate to is not crypto-friendly, we recommend checking out endaoment.org. They are a 501c(3) that enables on-chain donations to any US-based 501c(3) via a Donor Advised Fund (DAF). This method can also be done fully on-chain, so the donations never touch your personal wallet.

---

## How can I donate to charity?

Here are a few donation options:

**1)** On-chain donations through Endaoment.org

Endaoment is a 501c(3) organization that accepts crypto and distributes donations to any US-based 501c(3) charity in good standing with the IRS. Donations through Endaoment are set at the contract level and automatically routed at the time of payment without touching your wallet (and potentially avoiding tax liability).

To use Endaoment, go to Endaoment.org and create a fund. Then, enter ndao.eth in the additional payee field. Once you’ve created the fund, contact Dan (Druid#4611 on Discord) with your fund’s URL and project number. Once your project launches and the money is in your Endaoment Fund, you can send donations in any amount to any charity in the US. Many artists prefer this route so they can support many charities with smaller donations rather than one charity with one large donation. Please note - Endaoment charges 1.5% to receive, convert, and send money to a charity.

**2)** Create a second wallet

If you’d like to create a second wallet separate from your personal wallet, you can enter the wallet's address in the additional payee field to collect the total donation amount you intend to donate.

**3)** Receive funds in your primary wallet

If you’d like to receive all funds from your project’s sale in your primary wallet, that’s fine, but please communicate the total donations with Art Blocks and the community. Please be aware that receiving money in your personal wallet may incur tax obligations and reduce the total donation amount.

---

## How do I remove charitable giving information from the additional payee field mid-Dutch Auction?

If charity information is entered as an additional payee field and you would like to remove this information prior to decreasing your tier below 0.25 ETH, please adjust the additional payee field to either 0x0000000000000000000000000000000000000000 or to your own wallet address and adjust the additional payee percentage to 0% before submitting the next price tier. These fields cannot be blank once the dutch auction has begun.

---

## Where can I learn more about best practices for security, including hardware wallets?

Great question! We recommend that all users have a hardware wallet (typically Ledger or Trezor) that you use to interact with MetaMask.

You can learn more about security in the NFT space [here](https://medium.com/the-link-art-blocks/how-to-secure-your-collection-3dca5c073aef) (how to keep your collection safe) and [here](https://medium.com/the-link-art-blocks/avoiding-scams-and-staying-safe-9a6808a4146e) (how to avoid scams).

You can also check out our [After Dinner Mints episode](https://www.youtube.com/watch?v=u8MK99grAfI) dedicated to security!

---

## Is there a place I can connect with other artists and chat?

All artists are added to the artist-exclusive #artist-general channel in Discord where you can interact with other Art Blocks artists, share projects, and ask questions. We also encourage artists to participate in our Discord community. If you're selected for a curated drop, you'll have your own artist channel dedicated to focused discussions on your work. If you're selected for a factory drop, you can chat with artists and collectors in the #factory-projects channel.

---

## When will I know when my drop is scheduled? When will the drop be announced?

Once your application is approved, it takes approximately 5-6 weeks to reach a launch date for your project. You'll work closely with our team to schedule a drop date, which typically will be about 2 weeks after your project is finalized on main net. Every Friday, our team announces the following week's projects in the Discord channel, #upcoming-projects.

---

## Can I mint pieces of my own artwork? How many?

All artists on Art Blocks will mint the first piece (mint #0) of the collection for themselves. If you collaborated with other artists, you can each mint one of the first outputs before the project goes live.

If you're dropping in the Playground or Factory and you'd like to mint more pieces of the collection (for gifts or giveaways), reach out to our Artist Liaison, Sarah.

However, we ask that you clearly communicate why you're minting more than one to the community.

---

## How long do I need to wait before releasing a project through Art Blocks again?

We require artists to take a 2 month cool off period between drops in the Playground and Factory. In addition, there is a 6 month cool-off period between considerations for Curated projects. The cool off period begins when your project sells out (i.e. when minting is 100% completed).

---

## Will I have access to my testnet shell during my cooldown period?

Yes you will and we encourage you to use your testnet shell during your cooldown period. We kindly ask that you wait to ask for thumbnail refreshes if needed until after your cooldown period to limit noise on our end.

---

## What is the process upon returning to Art Blocks as a Factory artist?

As a next step in your Art Blocks journey, you will have a two month cooldown period before being eligible to submit another project. Your two month cooldown starts the day that your project sells out (i.e., when minting is 100% completed). After this period, you will be eligible to submit your next project to Art Blocks. We ask that you keep track of this timing on your end and please reach back out to us if you’d like to submit a project again after this time. You will continue to have access to your testnet shell during this time, so feel free to use that during your cooldown period.

Should you return, you'll submit a brief form with information about your proposed project. Once filled out, your project will be screened internally by our team via your testnet shell. Screenings occur weekly, so there will not be an extensive waiting period here. In our review, we will focus on overall aesthetics, variety in mints, and the degree to which a project explores new territory technically, visually, and conceptually. Based on this review, you will either move forward from there or we will ask that you take a one month development period before returning with a new project for screening.

This will be in addition to the curation review. This screening will be done by members of Art Blocks' team. Following that screening, accepted projects will then be viewed by our Curation Board as well. Right now this screening step takes place for new artists and is part of our application onboarding process, so the big change here is just that returning Factory artists will be starting at that step rather than fast-tracking to the Curation Review. This initial screening will also be an opportunity for Art Blocks' team to provide more direct feedback on newly proposed projects.
