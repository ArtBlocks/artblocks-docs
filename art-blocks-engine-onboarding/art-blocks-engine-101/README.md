# Art Blocks Engine 101

---

Interested in learning about an Art Blocks Engine partnership? Email engine@artblocks.io to get the conversation started! 

---

A high-level process map for Art Blocks Engine onboarding.

1. After the terms of engagement are finalized, you’ll sign the Engine service and setup agreement.
2. Provide the following information to Art Blocks for your Engine project:
   1 The admin address to own these contracts. This address controls the core contract and the minter contract.
   2 The name of tokens from your contract (e.g. for Art Blocks it is "Art Blocks" https://etherscan.io/address/0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270#code).
   3 The ticker for tokens from your contract (e.g. for Art Blocks it is "BLOCKS" https://etherscan.io/address/0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270#code).
3. Art Blocks' will deploy a set of testnet smart contracts for your team to begin integrating with.
   * After testnet deployment, there are two steps that may proceed in parallel.
     1. Your team can integrate your front end to allow for minting via your new Engine smart contract (using deployed Engine smart contracts).
     2. Art Blocks will need to integrate your newly deployed testnet smart contracts with our rendering infrastructure on testnet. After that, your team will connect to the staging site https://artist-staging.artblocks.io and interact with projects on the testing network you created as if they were on Art Blocks.
        * An ETA for this infrastructure integration piece will be given at the time of testnet contract deployment. On average, this will take 1 week from the time of testnet deployment.
        * To create a new project shell, you should use the addProject method of your newly deployed Engine Core Contract. This can be done by connecting to the contract via Etherscan.
4.  Your team will integrate a custom web frontend with your deployed Engine smart contracts (e.g., implementing their own purchase + display flow) and with the Art Blocks API as needed. An example of frontend purchase flow logic is provided here as a reference for integrating partners:

<details>
  <summary>Example frontend purchase flow logic in JavaScript</summary>
  
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
</details>
   

   5. Your team will use https://artist-staging.artblocks.io site to upload your project script source code and configure all project metadata details:
- project description
- the license associated with outputs
- artist website
- etc.

   If you need help, the Art Blocks team will help guide you through the process.

6. After you've set up and tested an Engine project, you can request a script audit from Art Blocks to guarantee resolution-agnosticism and determinism. 

**Warning:** if you opt-out of this step, it may result in undiagnosed issues with the rendered outputs. An unaudited project may not conform to the Art Blocks resolution-agnostic and deterministic standards. This means outputs may differ between screen sizes, devices, and operating systems or could be different from view to view.


7. After the complete end-to-end integration has been vetted on testnet, the above process may proceed on mainnet. 

Vetting includes minting in (1) each minting format, (2) from the Engine partner's frontend minting experience, and (3) while integrated with the Art Blocks' provided rendering infrastructure.


8.** Repeat steps 2-7 for mainnet deployment.** 
   
In summary, mainnet deployment entails:
- Deploy mainnet contracts.
- Integrate mainnet contracts with Art Blocks' rendering and API infrastructure.
- Update your mainnet website to reference deployed mainnet contracts.
- Create a new mainnet project shell on your smart contract using `addProject,`  and upload all project details and project script using the artist interface at `https://artblocks.io.`
- Mint at least one piece (mint #0) in a controlled environment on mainnet, being sure to mint in each format you plan to for your open release.

   9. After the above has all been performed, you should run through the following "pre-flight" checklist and ensure there are no loose threads:
   * If accepting ETH, check that the wallets **are not** multisig wallets like Gnosis Safe (check the minter owner, rendering provider, artist, and any additional payee).
     * **Note: **It is possible to use multisig wallets if our client's front-end properly populates access lists in their front end, but minting from Etherscan will not work.
   * **Important for mainnet**: Test-mint a token in each currency that will be accepted for a project. Verify that your front end is used to successfully mint using each currency to ensure a proper end-to-end test.
   * If actions of whitelisting/removing minters are expected, test those actions.
   * If actions of changing max invocations are expected, test those actions.
   * When using your front-end to mint, ensure at least a 10% margin is added to each transaction's [estimated Gas Limit](https://docs.ethers.io/v5/api/providers/provider/#Provider-estimateGas), as originated by your frontend logic.
     * If a 0% margin is used during a live NFT sale, the blockchain state will likely change between a user-submitted transaction and when it's mined. Therefore, small changes in the required Gas Limit will likely result in transaction failures if the gas necessary increases.

   10. You are now ready to sync with the Art Blocks team on planning for a launch date, which is **at least 1 week** from when the above steps have all been completed.
