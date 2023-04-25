---
order: -10
---

# Minter Suite Supplemental Information

This page provides supplemental information for the Art Blocks Minter Suite, which enables artists to choose how they distribute their artwork to collectors on a per-project basis.

!!!info
V3 Engine core contracts are able to use the Art Blocks Minter Suite by default, however the Engine minter suite does not currently support indexing in the Art Blocks subgraph and api. Work is underway to add this functionality, but in the interim, additional information may be provided on this page to help partners successfully use the Art Blocks Minter Suite.
!!!

## Allowlist Minter

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
