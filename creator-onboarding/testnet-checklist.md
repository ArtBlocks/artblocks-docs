---
order: -50
description: Staging Checklist
---

# Staging Shell Checklist

!!!danger
For Accepted Artists: Ask questions in the Discord DM titled [G_] the Art Team provided to you
For Applying Artists: Ask questions in  #artist-applications on Art Blocks’ Discord Server 
!!!

## Connect Your Wallet 

Within your MetaMask plugin, change your network to “Goerli Test Network”. You should see this as a drop-down option at the top of your MetaMask window. **[Note: If you do not see this drop-down as an option, please go to Account > Settings > Advanced and toggle “Show test networks” to YES. Once toggled to YES, you should see Goerli Test Network and others as a drop-down option.]**

Go to https://artist-staging.artblocks.io/

Click the Connect button in the upper right corner if you are not already connected, and sign the presented transaction. If you are not connected when accessing project pages, a 404 error will appear.

Note: For your Art Blocks application, please connect with a hot wallet. Hardware wallets are not currently compatible with Art Blocks staging.

## Upload

1. Please ensure that you have reviewed and abided by our [Documentation](readme/readme.md#documentation) and [Guidelines & Constraints](readme/readme.md#guidelines-and-constraints). Suppose you are assigning rarity to different things. In that case, Art Blocks strongly recommends using an instance of the Random class found [here](readme/readme.md#safely-deriving-randomness-from-the-token-hash) to feed all of your project's randomness. Before uploading, please verify that your script meets this requirement.

2. Ensure your wallet is funded with enough Goerli ETH to pay the gas fees for the upload and unpausing process. You can harvest Goerli [here](https://goerlifaucet.com/). 

3. Submit one field at a time. Wait for that transaction to clear before attempting the next field.

4. Upload your script. Guide to uploading your script can be found in the [Project Form Fields Guide](https://docs.artblocks.io/creator-docs/creator-onboarding/readme/project-form-fields-guide/#script)

## Test Minting

1. Before minting, go to the `minter` tab and set the minter to `Set Price - ETH (V2)`. Set the `base price` low as to not waste GoerliEth. 

<img width="1872" alt="01_minting" src="https://user-images.githubusercontent.com/103667291/214971637-38b650ff-5464-48b1-92b3-8725ce0841b6.png">

2. After you `submit` the minter to `Set Price - ETH (V2)` and entered the `base price`, go back to your project page and scroll down. 

<img width="1416" alt="Screenshot 2023-07-18 at 2 51 24 PM" src="https://github.com/ArtBlocks/artblocks-docs/assets/103667291/d9186cd6-ef93-49fa-8e77-9e0bbc919d42">

3. You will find the button that says `Artist Mint.` By pressing this button, you can mint outputs without unpausing your project. 

<img width="1866" alt="03_minting" src="https://user-images.githubusercontent.com/103667291/214972116-80a024f0-257c-4c37-a99b-597e732b7bf0.png">

4. Press `PURCHASE`.

<img width="1898" alt="04_minting" src="https://user-images.githubusercontent.com/103667291/214972204-b7cfe8f6-96f9-494c-96a4-f5403f66e066.png">

5. Success! You've minted your first test output. In order for your project shell to be reviewed by the internal screening committee, you will need to mint 50-70 test outputs. 

<img width="1900" alt="05_minting" src="https://user-images.githubusercontent.com/103667291/214972489-538b0842-f897-4562-8537-6ff36094e2d3.png">

## Features

Please see [Features](readme/features.md) for full details on how you set your project features as an artist.

## Add your project description 
The project description is an opportunity for you to highlight your intentions and provide an interpretative frame around how you want the viewer/collector to approach your project. For this reason, we find it very important. We have a series of prompts to help artists get started with this. Here is a suggested guideline. 

• Begin with a strong, clear opening sentence.

• Lead with the artistic inquiry; what questions can be prompted or answered through this work?

• How would you describe this project to someone unfamiliar with your work?

• What inspiration, color palette influences, themes, and techniques were used?

• Examine the outputs. What can the viewer see?

• Be sure to describe any interactivity features, if applicable.

• End by summarizing how the medium, outputs, and algorithm achieve your initial inquiry or concept.

## Updating your script 
If you make changes to your script, you may individually refresh your tokens. If you’ve refreshed your tokens, but do not see changes reflected, make sure that you have cleated your cache.
