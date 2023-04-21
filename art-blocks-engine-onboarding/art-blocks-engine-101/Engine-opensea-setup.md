---
order: 500
---
# Art Blocks Engine OpenSea Setup

Setting up the OpenSea storefront for your Art Blocks Engine contract.

## OpenSea Storefront Ownership Transfer

After the first token has been minted on your new Art Blocks Engine contract, you should be able to see this token in the OpenSea storefront. You will find this in the format `https://opensea.io/assets/{CONTRACT_ADDRESS}/{TOKEN_ID}` e.g. https://opensea.io/assets/0x13aae6f9599880edbb7d144bb13f1212cee99533/1000167.

Once this first token is populated, the Art Blocks team will be able to transfer the OpenSea collection for your project to a wallet that you control. By default, the Art Blocks team will plan to use the same address for the OpenSea collection ownership as it is designated to be the admin of your smart contract. However, if you prefer that a different wallet address manages the OpenSea collection, please reach out to Art Blocks to request this **before** the project has been transferred to your team.

After your OpenSea collection has your designated wallet added as the collection administrator, you may remove the wallet that Art Blocks controls from being an additional admin. It’s added automatically at the time of collection creation based on the contract deployer wallet address at the time of collection creation. **We recommend that you do so. That way, only you control your OpenSea storefront.**

Please contact the Art Blocks and/or OpenSea teams if you have any issues during this process.


## OpenSea Storefront Options

For Art Blocks Engine projects, there are two options that OpenSea can provide for collection organization:

   1\. All projects are grouped in one large collection, where individual projects within a collection are shown as filter traits on the sidebar of the OpenSea UI.

![All projects in one collection.](/static/screenshot1.png)

   2\. Each new project on your contract is handled as its own collection on OpenSea, where project traits are properties.

![Each project as its own collection.](/static/screenshot2.png)

By default, collections are organized via method 1. above. However, if you would like your collection to be handled via method 2., please reach out to the Art Blocks team, and we can facilitate this change by OpenSea on your behalf.
