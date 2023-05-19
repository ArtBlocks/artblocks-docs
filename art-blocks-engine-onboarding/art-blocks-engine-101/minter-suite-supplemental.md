---
order: -10
---

# Minter Suite Supplemental Information

This page provides supplemental information for the Art Blocks Minter Suite, which enables artists to choose how they distribute their artwork to collectors on a per-project basis.

!!!info
V3 Engine core contracts are able to use the Art Blocks Minter Suite by default, however the Engine minter suite does not currently support indexing in the Art Blocks subgraph and api. Work is underway to add this functionality, but in the interim, additional information may be provided on this page to help partners successfully use the Art Blocks Minter Suite.
!!!

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

This is a 2-step provess, and requires admin-intervention for security:

1. ADMIN - Call `resetAuctionDetails` on the minter contract
2. ARTIST - Configure the auction parameters via your typical process (e.g. artist dashboard)

### 3. Communicate and enjoy!

Ensure your collectors are aware of the new auction parameters, and enjoy the new auction!

---

## Allowlist Minter Details

The Allowlist Minter uses a Merkle tree to gas-efficiently allow a set of addresses to mint tokens from a project.

Merkle trees are a data structure that allow for efficient verification of whether a given element is contained in a set. In the case of the Allowlist Minter, the Merkle root is stored on-chain, and Merkle proofs are included with every purchase transaction to verify that a given address is allowed to mint a token.

!!!info
The information below is included to assist Engine partners in using the Allowlist minter with their projects. Eventually, the Art Blocks subgraph and api will be updated to index Engine minter suite data, at which point this information will be deprecated.
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
