---
# route: /creator-docs/powered-by-art-blocks-pbab-onboarding/pbab-101/
---
# PBAB 101

A high level process-map for PBAB onboarding.

1. Complete and sign copies of the formal PBAB service and setup agreements, which should be provided to you by Art Blocks after a business engagement has been agreed upon.
2. Provide the following information to Art Blocks for your PBAB project:
   1. The address that you would like to have own these contracts (admin for the Core contract and the owner for the Minter).
   2. The name of tokens from your contract (e.g. for Art Blocks it is "Art Blocks" https://etherscan.io/address/0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270#code).
   3. The ticker for tokens from your contract (e.g. for Art Blocks it is "BLOCKS" https://etherscan.io/address/0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270#code).
3. Art Blocks' will deploy a set of Ropsten smart contracts for your team to begin integrating with.
   * After Ropsten deployment, there are two steps that may proceed in parallel.
     1. Partner team can integrate their frontend to allow for minting via their PBAB smart contract (using deployed Ropsten smart contracts).
     2. Art Blocks will need to integrate deployed Ropsten smart contracts with the Art Blocks rendering infrastructure on Ropsten, after which partner teams will be able to connect to the https://artist-staging.artblocks.io site and interact with projects on the Ropsten network that they have created on their PBAB smart contract, as if they were projects on Art Blocks itself (e.g. upload source code, set features, set project metadata, etc.).
        * An ETA for this infrastructure integration piece will be given at the time of Ropsten contract deployment. On average, this will take 1 week from the time of Ropsten deployment.
        * To create a new project shell, partners should use the `addProject` method of their newly deployed PBAB Core Contract. This can be done by connecting to the contract via Etherscan.
4.  Partner team will integrate their custom web frontend with their deployed PBAB smart contracts (e.g. implementing their own purchase + display flow) and with the Art Blocks API as needed. An example of frontend purchase flow logic is provided here as a reference for integrating partners:

    ```js
    /** CONNECTION **/
    // A Web3Provider wraps a standard Web3 provider, which is
    // what Metamask injects as window.ethereum into each page
    const provider = new ethers.providers.Web3Provider(window.ethereum)
    // Connect to Dapp. This should happen in response to a user interaction
    await provider.send("eth_requestAccounts", []);
    // A signer is required to make any write transactions
    const signer = provider.getSigner();
    const userAddress = await signer.getAddress()

    /** PRE PURCHASE **/
    // Check that the project is unpaused, active, and
    // has not yet reached its maxInvocations. Also get
    // price per token.
    const genArt = new ethers.Contract('<CORE CONTRACT ADDRESS>', GEN_ART_ABI, provider)
    const { paused } = await genArt.projectScriptInfo('<PROJECT ID>')
    const { invocations, maxInvocations, pricePerTokenInWei, active, currencyAddress } = await genArt.projectTokenInfo('<PROJECT ID>')
    if (Number(invocations) >= Number(maxInvocations) || paused || !active) {
      // Disable purchase
      return
    }

    /** PRE PURCHASE (ERC-20) **/
    const NULL_ADDRESS = '0x0000000000000000000000000000000000000000'
    const projectUsesErc20 = currencyAddress && currencyAddress !== NULL_ADDRESS
    if (projectUsesErc20) {
      // Set up ERC-20 contract
      const erc20 = new ethers.Contract('<ERC-20 CONTRACT ADDRESS>', ERC20_ABI, signer)

      // Check that the user has the required amount of ERC-20
      const balance = await erc20.balanceOf(userAddress)
      if (balance.lt(pricePerTokenInWei)) {
        // Show insufficent funds error
        return
      }

      // Check allowance for minterAddress allowed by user
      const allowance = await erc20.allowance(
        userAddress,
        '<MINTER CONTRACT ADDRESS>'
      )

      // If the user has not yet allowed enough of their ERC-20 to be used
      // by the minter, have them approve enough.
      if (allowance.lt(pricePerTokenInWei)) {
        // Trigger user wallet dialogue. This should be done in response to user interaction.
        const approveTransaction = await erc20.approve('<MINTER CONTRACT ADDRESS>', pricePerTokenInWei)
        // Wait for approve transaction confirmation
        await approveTransaction.wait(1)
      }
    }

    /** PURCHASE **/
    // Set up minter contract connected to users wallet
    const minter = new ethers.Contract('<MINTER CONTRACT ADDRESS>', MINTER_ABI, signer);
    // Initiate purchase transaction (user must confirm through metamask).
    // If paying in ether, we must include a payable value otherwise payable value will be 0.
    const transaction = await minter.purchase('<PROJECT ID>', { value: projectUsesErc20 ? '0' : pricePerTokenInWei})
    // Wait for the transaction to be confirmed. The number passed to the wait function specifies the
    // number of block confirmations to wait for.  You may want to wait longer than a single
    // block to prevent showing the wrong output in case of a chain reorg. The Art Blocks site
    // waits for 3 block confirmations.
    const receipt = await transaction.wait(3)
    // Iterate through events to find mint event
    const mintEvent = (receipt.events || []).find(
      (receiptEvent) => {
        const event = genArt.interface.getEvent(
          receiptEvent.topics[0]
        )
        return event && event.name === 'Mint'
      }
    )

    // Decode the mint event
    const mintEventDecoded = genArt.interface.decodeEventLog(
      'Mint',
      mintEvent.data,
      mintEvent.topics
    )
    // Token ID as BigNumber object
    const tokenIdBigNum = mintEventDecoded['_tokenId']
    // Token ID as string
    const tokenId = tokenIdBigNum.toString()
    // Use the token id to display the newly minted token with the iframe'd generator
    ```
5. Partner team will use the https://artist-staging.artblocks.io site to configure all project metadata details (e.g. project description, license associated with outputs,  artist website) and upload their project script source code. This process looks very similar to the process within Art Blocks itself for creators uploading their projects, so "[Art Blocks 101 for Creators](/readme.md#documentation)" should provide a good reference for this process, but the Art Blocks creative team will also be able to assist in this process.
6. Once this process has been fully completed for the "project 0" (the first project) of the PBAB partner's platform, optionally an audit may be performed by the Art Blocks team to guaruntee resolution-agnositicism and determinism. Warning: if a PBAB partner determines that they would prefer to opt-out of this step, it may result in there being issues with the rendered outputs provided for said project (e.g. they perform differently on different screen sizes, or are different from view-to-view) due to not conforming to Art Blocks' standards for resolution-agnositicism and determinism.
7. After the entire end-to-end integration has been vetted (minting in each minting format, from the PBAB partner's frontend minting experience, while integrated with the Art Blocks' provided rendering infrastructure, etc.) on Ropsten, the above process may proceed on mainnet.
8. Repeat the above process, for mainnet deployment. In summary, this is:
   1. Deploy mainnet contracts.
   2. Integrate mainnet contracts with Art Blocks' rendering and API infrastructure.
   3. PBAB partner to update their mainnet website implementation to refer to deployed mainnet contracts.
   4. PBAB partner to create a new mainnet project shell (using `addProject`) and partner artist to upload all project details and project script using the artist interface at https://artblocks.io.
   5. PBAB partner artist to perform mint #0 (or #0, and #1, and #2, etc.) in a controlled environment on mainnet, ensuring that they mint in each format they plan to for their open release.
9. After the above has all been performed, the PBAB should run through the following "pre-flight" checklist and ensure there are no loose threads:
   * If accepting ETH, check that the wallets of the minter owner, render provider, artist, and any additional payee are not multisig wallets (like Gnosis Safe).
     * **Note: **It is possible to use multisig wallets if our client's front-end properly populates [access lists](https://docs.ethers.io/v5/api/providers/types/#providers-AccessList) in their front end, but minting from Etherscan will not work.
   * **Especially important for mainnet**: Test-mint a token in each currency (e.g. if ETH is used for part of the sale, and some custom ERC20 is used for a separate part of the sale) that will be accepted for a project. Ensure that the PBAB partner's front-end is used to accomplish each mint to ensure a proper end-to-end test.
   * If actions of whitelisting/removing minters are expected, test those actions.
   * If actions of changing max invocations are expected, test those actions.
   * When using PBAB's front-end to mint, ensure at least a 10% margin is being added to each transaction's [estimated Gas Limit](https://docs.ethers.io/v5/api/providers/provider/#Provider-estimateGas), as originated by the partner's fronend logic.
     * If 0% margin is used, during a live NFT sale, blockchain state is likely to change between when the user submits a transaction and when it is mined. Small changes in required Gas Limit are likely and will result in TX failure if required gas goes slightly up.
10. You are now ready to sync with the Art Blocks team on planning for a "go live" date, that is at least 1 week out from the time the above steps have all been completed.
