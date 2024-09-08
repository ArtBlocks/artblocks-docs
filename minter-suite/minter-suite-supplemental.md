---
order: -10
---

# Minter Suite Supplemental Information

This page provides supplemental information for the Art Blocks Shared Minter Suite.

The information below is generally most relevant for Engine core contract admins.

---

## Auction Reset Process

A subset of minters utilize automated, scheduled auctions to distribute artwork to collectors. The auction reset process is a mechanism that allows artists to pause and reschedule their auction, within certain limitations, if an issue arises during a live project release. Example situations may be:

- Unexpected website downtime
- Artist unintentionally left project in a paused state
- Auction parameters were not set as intended

Some of the possible failure modes above can result in a state where:

- Collectors are not able to purchase tokens from the website
- Bots are still able to purchase tokens by submitting transactions directly to the blockchain

If in a state where bots can purchase but humans can not, the situation requires immediate action to prevent or minimize damage.

### 1. [URGENT] Pause the Auction

The most important step in the auction reset process is for the Artist pause the auction. This prevents any further purchases from being made.

Tips:

- Ensure that the project is not already paused (i.e. this step is already complete), and do not toggle the pause button more than once (i.e. pause then unpause)
- Artist should use a very high gas price to ensure that the pause transaction is mined quickly
- Artist should use a tool like [Etherscan](https://etherscan.io/) to monitor the status of the pause transaction
- Verify the paused state of the contract by checking the project's core contract on a tool like [Etherscan](https://etherscan.io/)

!!!danger
**DA with Settlement:** This step is especially urgent! Settlement minters require that every new purchase price is less than or equal to the previous purchase price (even after an auction is reset). If a bot purchases a token prior to a project being paused, that project’s reconfigured auction (even after reset) is constrained to only be able to start at the bot’s purchase price.
!!!

### 2. Reset auction

When using a Dutch auction, the auction will need to be reset and reconfigured.

This is a 2-step process, and requires admin-intervention for security:

1. ADMIN - Call `resetAuctionDetails` on the minter contract
2. ARTIST - Configure the auction parameters via your typical process (e.g. artist dashboard)

### 3. Communicate and enjoy!

Ensure your collectors are aware of the new auction parameters, and enjoy the new auction!

---

## Allowlist Minter Details (non-shared minter suite only)

The Allowlist Minter uses a Merkle tree to gas-efficiently allow a set of addresses to mint tokens from a project.

Merkle trees are a data structure that allow for efficient verification of whether a given element is contained in a set. In the case of the Allowlist Minter, the Merkle root is stored on-chain, and Merkle proofs are included with every purchase transaction to verify that a given address is allowed to mint a token.

!!!info
The information below is included to assist Engine partners in using the Allowlist minter with their projects. However, if using the shared minter suite, the Art Blocks subgraph and api are available to index Engine minter suite data, and this information is not required.
!!!

**Fundamentals**

The Merkle allowlist minter follows the following basic process:

- An allowlist of wallet addresses is stored off-chain (e.g. in a csv file)
- The artist uploads the Merkle root of the list of addresses to the Minter contract via function `updateMerkleRoot`
- Collectors calculate and include a Merkle proof with their purchase transaction to verify that their address is included in the allowlist

**Example Usage**

The following typescript code demonstrates how a Merkle root and proof may be calculated for a given allowlist:

```typescript
// npm install merkletreejs
import { MerkleTree } from "merkletreejs";
// npm install ethers
import { keccak256, solidityKeccak256 } from "ethers/lib/utils";

const hashAddress = (address: string) => {
  return Buffer.from(solidityKeccak256(["address"], [address]).slice(2), "hex");
};

export const getMerkleRoot = (addresses: string[]): string => {
  const merkleTree = new MerkleTree(
    addresses.map((addr: string) => hashAddress(addr)),
    keccak256,
    { sortPairs: true }
  );
  const root = merkleTree.getHexRoot();
  return root;
};

export const generateUserMerkleProof = (
  addresses: string[],
  userAddress: string
): string[] => {
  const merkleTree = new MerkleTree(
    addresses.map((addr) => hashAddress(addr)),
    keccak256,
    {
      sortPairs: true,
    }
  );
  return merkleTree.getHexProof(hashAddress(userAddress));
};

///////////////////////////////////////////////////////////////////////////////
// EXAMPLE USAGE
///////////////////////////////////////////////////////////////////////////////

// allowlist could be fetched from a database or a file
// example allowlist addresses
const allowlistAddresses = [
  "0xaE839a65A8AA0E54323d7Eda4c5d77562fCBCBC0",
  "0x9d688d290d9CdD2a8f8040B48C6d40d039B2b8ba",
  "0x4CFA1e7a4cF5Eb5a0Dd0460F431d8e96155d8611",
  "0x09e2978EF8638CBc564D2E34325734B42F654DBe", // ... and so on
];
console.log("Allowlist addresses: ", allowlistAddresses);

// Generate the Merkle root for artist to upload to the minter contract
const merkleRoot = getMerkleRoot(allowlistAddresses);
console.log("Merkle root: ", merkleRoot);
// Generate the bytes32[] Merkle proof for a user to be included in the purchase transaction
// example user address: 0xaE839a65A8AA0E54323d7Eda4c5d77562fCBCBC0
const merkleProof = generateUserMerkleProof(
  allowlistAddresses,
  "0xaE839a65A8AA0E54323d7Eda4c5d77562fCBCBC0"
);
console.log(
  "Merkle proof for 0xaE839a65A8AA0E54323d7Eda4c5d77562fCBCBC0: ",
  merkleProof
);
```

---

## Pre-Assigning Token Hash Seeds

!!!info
The shared randomizer `SharedRandomizerV0` enables an artist to pre-assign token hash seeds for tokens on a project. This allows an artist to assign a specific hash seed to a token before it is minted, and then mint the token with that hash seed at a later time.
!!!

The process for pre-assigning token hash seeds is as follows:

1. Identify and confirm that your contract is using a `SharedRandomizerV0` contract. Visit your core contract on etherscan (or appropriate L2 explorer, e.g. basescan) and inspect the read-only function `randomizerContract()` to confirm that the randomizer contract is a `SharedRandomizerV0`.

1. Navigate to the `SharedRandomizerV0` contract on etherscan (or appropriate L2 explorer, e.g. basescan), and connect your artist wallet. Alternatively, if your artist wallet is a multisig, interact with the `sharedRandomizerV0` in something like Gnosis Safe's Transaction Builder (this is more efficient and convenient when assigning hash seeds for many tokens).

1. On `SharedRandomizerV0`, call the `toggleProjectUseAssignedHashSeed()` function with the artist wallet the following parameters:

   - `coreContract`: The address of the core contract for the project
   - `ProjectId`: The ID of the project to toggle the use of assigned hash seeds for

1. Confirm on `SharedRandomizerV0`'s read function `projectUsesHashSeedSetter()` that the project is now configured to use pre-assigned hash seeds (should return `true`).

1. On `SharedRandomizerV0`, from the artist wallet, call to the `setHashSeedSetterContract` function with the following parameters:

   - `coreContract`: The address of the core contract for the project
   - `ProjectId`: The ID of the project to toggle the use of assigned hash seeds for
   - `hashSeedSetterContract`: The address that will assign hash seeds to tokens - recommend in this use-case to set this to the artist wallet

1. Confirm on `SharedRandomizerV0`'s read function `hashSeedSetterContracts()` that the hash seed setter contract is now set to the artist wallet for the project.

1. On `SharedRandomizerV0`, from the artist wallet, call `preSetHashSeed()` for each token that you want to assign a hash seed to (Multicall using something like a gnosis safe is very helpful if assigning many tokens here). This function takes the following parameters:

   - `coreContract`: The address of the core contract for the project
   - `tokenId`: The token ID to assign the hash seed for
   - `hashSeed`: The hash seed to assign to the token

1. You may confirm that token hash seeds have been properly assigned by calling the `preAssignedHashSeed()` read-only function on `SharedRandomizerV0` with the following parameters:

   - `coreContract`: The address of the core contract for the project
   - `tokenId`: The token ID to check the hash seed for

1. MINT! Ordering may be critical if minting specific tokens to specific addresses, so the artist may need to keep the project paused and call purchaseTo in a specific order. No other changes to the minting process are required. Confirming token hashes are as expected along the way is highly recommended.

1. After minting is complete, the artist should call `toggleProjectUseAssignedHashSeed()` to disable the use of assigned hash seeds for the project, and allow the randomizer to pseudorandomly assign hash seeds to tokens as normal.

1. Set the hash seed setter contract back to the zero address by calling `setHashSeedSetterContract` from the artist wallet.

!!!info
The steps above follow the pattern implemented in the following test case: [shared-randomizer-v0/configure.test.ts:assigns_expected_token_when_polyptych"](https://github.com/ArtBlocks/artblocks-contracts/blob/1d2a6ad5915cb225c6b0d31710568a439b0e212b/packages/contracts/test/randomizer/shared-randomizer-v0/configure.test.ts#L269)
!!!
