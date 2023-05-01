---
order: 400
---

# Mobile Minting for In-Person Activations

The Art Blocks Mobile Minter is a specialized app for iPad and iPhone designed to streamline the minting process during in-person events. Unlike the standard Art Blocks website, which is accessible from any device, the Mobile Minter is tailored for events where minting is exclusive to attendees or offered as an event gift.

### Features

The Mobile Minter is capable of:

- Minting Art Blocks tokens with a pre-funded wallet to cover gas fees
- Minting tokens to an ENS name or a copied Ethereum address
- Authenticating users with FaceID/TouchID for quick access during live events
- Minting tokens without requiring manual signing and submission of Ethereum transactions

### Requirements

The Mobile Minter is perfect for situations where:

- A project is paused and not available for online minting
- An artist wants to distribute their work at a live event
- An iPad or iPhone with the latest iOS version is available
- A small amount of Ethereum is on hand to cover gas fees for token recipients
- You've set up a Stripe account to accept fiat payment (optional)

---

## Getting Started

To use the Mobile Minter, follow these steps to set up your project and device according to the system requirements.

### Step 1. Project Configuration

<aside>
⚠️ If you're already an Art Blocks Engine customer using the Mobile Minter admin dashboard, the project configuration can be completed by the admin.
</aside>

To set up the Mobile Minter for your project:

1. [Send a Slack message in Slack](https://app.slack.com/client/T02TTJYK6G1/C03DHF7ERRT) requesting access to the Mobile Minter
2. Art Blocks staff (@Shantanu Bala) will provide a wallet address that will be used to pay for gas fees for transactions
   _Note: The app manages this wallet, and any remaining funds can be returned to you at any time_
3. Pause your project to restrict minting to the artist only
4. Transfer artist ownership to the wallet address from Step #2, making the Mobile Minter the sole minting wallet for the project
5. After completing these steps, Art Blocks staff (@Shantanu Bala) will give you login details to start using the mobile app

### Step 2. Device Setup

To prepare your mobile device:

1. Update your iPhone or iPad to the latest iOS version
2. Set up and ensure FaceID or TouchID is functional on your device
3. Download the TestFlight app from the App Store: [TestFlight](https://apps.apple.com/us/app/testflight/id899247664)
4. [Join the Mobile Minter beta](https://testflight.apple.com/join/SlbRPkXG) on TestFlight:
5. Sign in, set up FaceID, and proceed to minting

### Step 3. Minting

[![Youtube Thumbnail](https://img.youtube.com/vi/mBOdGxz9tdM/0.jpg)](https://youtu.be/mBOdGxz9tdM)

Click the image above to view a screen recording of the Mobile Minter app on iPad. This test demonstrates the steps to mint a project on the Goerli test network. To mint a new token, users follow these steps:

1. Open the Mobile Minter app on an iPhone or iPad device
2. Sign in using FaceID
3. Select a project from the list of available projects
4. Input an ENS name or wallet address
5. Confirm the minting details
6. Wait for the token minting transaction to be confirmed

---

## Payment Processing

The Mobile Minter utilizes [Stripe Terminal](https://stripe.com/terminal) for handling payments. Art Blocks does not offer merchant accounts or handle tax remittance for partners. To process fiat payments with Stripe Terminal, all Art Blocks Engine partners must [create and configure their own Stripe account](https://dashboard.stripe.com/register).

The backend (Art Blocks Minting API) and point of sale (Mobile Minter app) software are provided by Art Blocks. However, the hardware must be procured by Art Blocks Engine customers.

### Stripe Reader M2

We recommend using the Stripe Reader M2 with the Mobile Minter due to its convenient NFC payment support, Bluetooth connectivity, long-term SDK support, and reliable chip/magstripe fallback. You will need to order the M2 directly from Stripe.

[Stripe Reader M2](https://stripe.com/docs/terminal/readers/stripe-m2)

### Direct Charges

The Mobile Minter uses Stripe Connect to make a [direct charge](https://stripe.com/docs/connect/direct-charges) using your Stripe account. Stripe Connect processes direct charges for your Art Blocks Engine project using your own Stripe account (connected account) while using our platform - note that the charge amounts and fees are mock examples provided by Stripe.

### Stripe API Secrets

**Do not share** your live Stripe API keys with anyone, including Art Blocks employees. Instead, Art Blocks will supply a secure OAuth link from Stripe for your usage. Connected accounts are managed using the process outlined by Stripe:

[Managing connected accounts with the Dashboard](https://stripe.com/docs/connect/dashboard)

---

## Displaying Live Mints

Web-enabled TVs or displays can showcase a real-time view of the latest tokens minted through the Mobile Minter. The Art Blocks documentation site offers an [overview of configuration options for the live viewer](https://docs.artblocks.io/creator-docs/art-blocks-api/artblocks-viewer/#artblocks-viewer).

### Example Embed

You can embed [live.artblocks.io](http://live.artblocks.io) using an iframe on a web page containing your organization’s branding.

[Example embed of [live.artblocks.io](http://live.artblocks.io) without any configuration parameters ([docs](https://docs.artblocks.io/creator-docs/art-blocks-api/artblocks-viewer/#artblocks-viewer))](https://live.artblocks.io/)

Example embed of [live.artblocks.io](http://live.artblocks.io) without any configuration parameters ([docs](https://docs.artblocks.io/creator-docs/art-blocks-api/artblocks-viewer/#artblocks-viewer))

---

## Frequently Asked Questions

### Can the Mobile Minter be used with projects that are not paused?

Yes, the Mobile Minter can be used for active projects. However, pausing the project and transferring artist ownership to the app restricts minting exclusively through the app. If a project remains unpaused, anyone online can mint tokens.

### Can users pay for gas fees themselves?

Currently, gas fees must be pre-funded by the artist or the organization using the Mobile Minter app, through the Mobile Minter's hot wallet.

### Can my prepaid gas fee balance be returned to me?

Yes, please contact us to arrange the return of any remaining funds to the original depositing wallet. To have the remaining ETH returned, ensure that the funds were initially transferred to the Mobile Minter's hot wallet from an address capable of receiving ETH on behalf of your organization. The unspent ETH can only be sent back to the original sender's wallet.

### Can multiple projects be managed simultaneously through the Mobile Minter app?

Yes, the Mobile Minter app allows you to manage multiple projects for in-person events. You can easily switch between projects during the event, ensuring a seamless minting experience for attendees.

### What currencies are supported for payments in the Mobile Minter app?

The Mobile Minter app processes fiat payments via Stripe Terminal, which supports a variety of currencies. The available currencies depend on your Stripe account and the country where your business operates. You will be the merchant of record, and Art Blocks will collect its platform fees in ETH or USD. For a list of supported currencies for your customers, please refer to the [Stripe documentation](https://stripe.com/docs/currencies).

### Is it possible to customize the appearance of the Mobile Minter app for my event?

While the Mobile Minter app does not offer customization, you can embed [live.artblocks.io](https://live.artblocks.io/) inside of a page that showcases your event's theme and branding. Please refer to the [Art Blocks documentation site](https://docs.artblocks.io/creator-docs/art-blocks-api/artblocks-viewer/#artblocks-viewer) for an overview of configuration options for the live viewer.
