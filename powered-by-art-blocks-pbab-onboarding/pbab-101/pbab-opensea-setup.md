---
order: 900
# route: /creator-docs/powered-by-art-blocks-pbab-onboarding/pbab-101/pbab-opensea-setup/
---
# PBAB OpenSea Setup

Setting up the OpenSea storefront for your Powered by Art Blocks project.

## OpenSea Storefront Ownership Transfer

After the first token has been minted on your new Powered by Art Blocks contract, you should be able to see this token in the OpenSea storefront. You will find this in the format `https://opensea.io/assets/{CONTRACT_ADDRESS}/{TOKEN_ID}` e.g. https://opensea.io/assets/0x13aae6f9599880edbb7d144bb13f1212cee99533/1000167.

Once this first token has been populated, the Art Blocks team will be able to transfer the OpenSea collection for your project over to a wallet that you control. By default, the Art Blocks team will plan to use the same address for the OpenSea collection ownership as is designated to be the admin of your smart contract. **If you would prefer that the OpenSea collection be managed by a different wallet address,** please reach out to the Art Blocks team to request this **before the project has already been transferred to your team.**

After your OpenSea collection has had your designated wallet added to be an administrator of the collection, you may remove the wallet that Art Blocks controls from being an additional admin, which is added automatically at the time of collection creation based on the contract deployer wallet address. We recommend that you do so, so that only you control your OpenSea storefront.

If you run into any issues during this process, please reach out to the Art Blocks and/or OpenSea teams!

## OpenSea Storefront Options

For Powered by Art Blocks projects, there are two options that OpenSea is able to provide for collection organization.

   1\. All projects are grouped in one single collection ("the old Art Blocks way"), where individual projects within a collection are shown as property dropdowns in the left sidebar of the OpenSea UI.

![All projects in one collection.](/static/screenshot1.png)

     2\. Each new project on your contract is handled as its own collection on OpenSea ("the new Art Blocks way"), where project traits are properties themselves.

![Each project as its own collection.](/static/screenshot2.png)

By default, collections are organized via method 1. above. If you would like your collection to be handled via method 2., please reach out to the Art Blocks team and we can facilitate this change being made by OpenSea on your behalf.
