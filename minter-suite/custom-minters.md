---
order: 850
---

# Custom, One-Off Minters

Some Engine partners may wish to add custom, one-off minters to the shared minter suite. This is able to be done by the admin of an Engine partner's core contract.

!!!info
Due to the high flexibility available to custom minters, they are not indexed by the Art Blocks subgraph, and therefore are not able to be configured by artists via the Art Blocks frontend. Instead, the custom minter will need to be configured via the Engine partner's frontend, etherscan, etc.
!!!

The steps to add a custom, one-off minter to the shared minter suite are as follows:

## 1. Write the custom minter contract

The Engine partner will need to write the custom minter contract. The Art Blocks team can assist with providing guidance on how to translate a previously written, non-shared custom minter contract to be compatible with the new shared minter suite, if needed.

At a minimum, the custom minter contract will need to implement the `ISharedMinterRequired` interface, which is available in the [Art Blocks smart contracts monrorepo](https://github.com/ArtBlocks/artblocks-contracts/blob/main/packages/contracts/contracts/interfaces/v0.8.x/ISharedMinterRequired.sol). This interface requires the custom minter contract to implement the following functions:

```js
interface ISharedMinterRequired {
    // Function returns the minter type, and is called by the MinterFilter for
    // metadata purposes.
    function minterType() external view returns (string memory);

    // Function returns the minter's associated shared minter filter address,
    // and is called by subgraph indexing service for entity relation purposes.
    function minterFilterAddress() external returns (address);
}
```

Additionally, the custom minter contract will need to call the `mint_joo` function on the shared minter filter contract to mint tokens. This function is included in the `IMinterFilterV1` interface in the [Art Blocks smart contracts monrorepo](https://github.com/ArtBlocks/artblocks-contracts/blob/7f0af6773fdd2c85ee33bfa5c3eeb39b57839131/packages/contracts/contracts/interfaces/v0.8.x/IMinterFilterV1.sol#L107).

```js
interface IMinterFilterV1 {
    ...
    // @dev function name is optimized for gas
    function mint_joo(
        address to,
        uint256 projectId,
        address coreContract,
        address sender
    ) external returns (uint256);
    ....
}
```

## 2. Deploy the custom minter contract

The Engine partner will need to deploy the custom minter contract to the desired network.

## 3. Allowlist the minter for the core contract on the shared minter filter contract

The Engine partner will need to allowlist the custom minter contract for their contract, on the shared minter filter contract. This is done by doing the following:

- Engine Admin calls `approveMinterForContract` on the shared minter filter contract, passing in the address of their core contract, and the custom minter contract

The custom minter is now ready to be used by projects on the Engine partner's core contract!

## 4. Artist configures the custom minter for their project

The artist will need to configure the custom minter for their project. Custom, one-off minters are not indexed by the Art Blocks subgraph (due to the minter being arbitrary and open-ended), so the artist will need to configure the custom minter via the Engine partner's frontend, etherscan, etc. Note that the typical minter filter function for setting a minter for a project, `setMinterForProject` should be used by the artist or admin to assign the custom minter for the project.
