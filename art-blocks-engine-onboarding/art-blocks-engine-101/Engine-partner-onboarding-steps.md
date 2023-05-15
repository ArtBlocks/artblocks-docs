---
order: 900
---
# Engine Partner Onboarding Steps

An overview of the steps required to onboard as an Art Blocks Engine partner.

## 1. Initial outreach

Interested in using Art Blocks Engine to launch a generative content platform?

Reach out to **info@artblocks.io** to get started. We'll discuss your needs, explain what we offer in a partnership, and align expectations.

[!badge Timeline: typically 1-2 weeks]

## 2. Project scope

The Art Blocks team will work with you to determine the scope of the Art Blocks Engine project.

[!badge Timeline: 1-2 weeks]

## 3. Contract agreement

Once the project objectives and scope are agreed upon, you'll work with our operations team to sign our partnership agreement.

[!badge Timeline: 1 week]

## 4. Smart contract details

To get started, you'll provide our team with:

- An Ethereum wallet address (that you currently own and control) you'll use to manage your Art Blocks Engine smart contracts
- The name you’ll use for tokens from your contract (e.g., for Art Blocks, it is "Art Blocks")
- The ticker symbol you’ll use for tokens from your contract (e.g., for Art Blocks, it is "BLOCKS")
- Deployment Type: V3 Engine or V3 Engine Flex
- [Minter Type](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/MINTER_SUITE.md#minter-suite-documentation): flat price eth only, set price custom erc20, merkle tree allowlist, holder-gated, linear DA, exponential DA, and exponential DA with settlement
- Starting project ID # (>=0):
- Set autoApproveArtistSplitProposals: true or false

Regarding "autoApproveArtistSplitProposals" - It needs to be set at deployment and cannot be changed later.

tldr - if true, artist royalty wallet changes are auto-approved. If false, the contract admin will need to approve the artist's royalty wallet changes. This is an added check to ensure your artists aren't changing royalty wallets to a random address, which could complicate accounting/ OFAC compliance.

Note: We cannot deploy your contract until you provide the above information. **The name and symbol tied to your contract cannot change once it’s deployed.**_

[!badge Timeline: 1-2 days]

## 5. Contract configuration & testnet deployment

We will configure your smart contract before transferring ownership to Ethereum address provided in Step 4. Once we deploy your contract on the test network, you can start testing your generative script.

[!badge Timeline: 1 week]

## 6. Testnet infrastructure integration

Art Blocks will integrate your contracts with our rendering infrastructure and provide access to our staging website for you to perform project onboarding and configuration via the Art Blocks site on the test network.

Contracts are deployed twice per month and typically take 1 week to complete and transfer.

[!badge Timeline: 1 week]

## 7. Integration with partner’s site

Your team will integrate your site’s front-end with the contract created by Art Blocks to test your outputs on the testnet.

[!badge Timeline: weeks-months (depends on partner)]
- [x] Connect your front end to testnet contracts

## 8. Test mints on partner site

Your team ensures the minting process is working on the test network by minting your NFTs using the front-end of your site.

[!badge Timeline: weeks-months (depends on partner)]
- [x] Mint test outputs
- [x] Test drop mechanic (flat price, Dutch Auction, whitelists, etc.)
- [x] Test purchase with custom ERC20 (if applicable)
- [x] Request a script audit from Art Blocks
- [x] Test your script across different hardware/software ([browserstack.com](https://www.browserstack.com/))
- [x] Let the Art Blocks team know testing is complete and you're ready for a mainnet deployment

## 9. Deployment to mainnet

Art Blocks deploys the mainnet version of your contract and integrates it with our infrastructure.

[!badge Timeline: 2 weeks]

## 10. Infrastructure integration (mainnet)

Your team integrates the mainnet contract with your site and prepares to generate your first NFT (mint #0)

[!badge Timeline: Depends on partner]
- [x] Connect your front end with the *new* mainnet contracts, using the same minting mechanics from testnet (drop type & currency)
- [x] Mint #0 from your front end


## 11. Mint #0

You can mint your project's first official token via your site!

## 12. Set secondary royalties

Art Blocks will set *our* secondary royalty before we transfer contract ownership, but you are responsible for setting your own secondary royalty across all secondary marketplaces.

OpenSea - https://docs.opensea.io/docs/10-setting-fees-on-secondary-sales
LooksRare - https://docs.looksrare.org/guides/collection-management/set-or-edit-collection-royalties
x2y2 - https://docs.x2y2.io/guides/collection-management/manage-your-collection

Note: The vast majority of secondary activity takes place on OpenSea. Currently, OpenSea does not recognize on-chain roylaties and needs to be set through their interface. However, they plan to recognize [Roylaty Registry](https://royaltyregistry.xyz/lookup) in the near-ish future. We highly encourage you to sign up for the Royalty Registry to avoid missed secondary roylaties.

Instructions on setting up Royalty Registry - https://docs.artblocks.io/creator-docs/art-blocks-engine-onboarding/art-blocks-engine-101/engine-royalty-registry-setup/


## 13. Project launch

You can choose a launch date for your project. Please allow at least one week between a successful mint #0 and a go-live date.

[!badge Timeline: 1 week from completion of step 11]
