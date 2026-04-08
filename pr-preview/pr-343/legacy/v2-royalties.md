# Legacy: V2 Royalty Registry Setup

!!!warning
This page applies only to **V2 Engine contracts** (deployed before May 2024). All current Engine deployments use V3.2+ contracts, which integrate automatically with ERC-2981 royalties via 0xSplits. See [Core Contract (V3)](/developer/core-contract/) for current royalty information.
!!!

V2 Engine contracts require a manual shim-layer configuration to integrate with the [Royalty Registry](https://royaltyregistry.xyz/lookup).

---

## Royalty Payment Addresses (V2)

| Party | Typical Royalty Percentage |
|---|---|
| Platform (Engine Partner) | default 2.5% |
| Render Provider (Art Blocks) | default 2.5% |
| Artist | typically 5%, configurable by artist |
| Additional Payee | split between Artist & Additional Payee |

---

## Required V2 Setup

!!!danger
**Do not use the [Royalty Registry's "Configure" UI](https://royaltyregistry.xyz/configure)** to configure royalties for Engine contracts. This will result in incorrect royalty payments across all projects on the contract. Follow the process below instead.
!!!

### A. Pre-setup

Ensure every project has the desired artist royalty percentage set on the Engine contract. Only artists may update their project's royalty percentage by calling:

```
updateProjectSecondaryMarketRoyaltyPercentage(<_projectId>, <_royaltyPercentage>)
```

The percentage represents the total paid to the artist + additional payee (typically 5). The 2.5% platform and 2.5% render provider shares are added by the override contract below.

### B. Royalty Registry Integration

**Step 1:** Create a new override on the Royalty Registry for your Engine core contract.

- View the Royalty Registry mainnet contract on Etherscan: [0xad2184fb5dbcfc05d8f056542fb25b04fa32a95d](https://etherscan.io/address/0xad2184fb5dbcfc05d8f056542fb25b04fa32a95d#writeProxyContract)
- Using "Connect to Web3," connect your Engine `admin` wallet on the "Write as Proxy" tab
- Call `setRoyaltyLookupAddress` with:
  - `tokenAddress`: Your Engine core contract address
  - `royaltyLookupAddress`: `0x31E1cC72E6f9E27C2ECbB500d978de1691173F5f` (Art Blocks Engine Royalty Registry override contract)

**Step 2:** Set your Platform royalty payment address.

- Connect your Engine `admin` wallet to the Art Blocks Engine royalty override contract: [0x31E1cC72E6f9E27C2ECbB500d978de1691173F5f](https://etherscan.io/address/0x31e1cc72e6f9e27c2ecbb500d978de1691173f5f#writeContract)
- Call `updatePlatformRoyaltyAddressForContract` with:
  - `_tokenContract`: Your Engine token contract address
  - `_platformRoyaltyAddress`: Your desired platform royalty payment address

You will now automatically receive royalties from secondary markets that support the Royalty Registry.

---

## Optional V2 Configuration

Default royalty percentages are 2.5% for both platform and render provider. The contract admin can override these by calling `updatePlatformBpsForContract` or `updateRenderProviderBpsForContract` on the override contract.

Royalty percentages are defined in basis points: 250 BPS = 2.5%.

The platform royalty payment address can be updated at any time by the admin by calling `updatePlatformRoyaltyAddressForContract` again.

---

## Verifying Configuration

Use the [Royalty Registry Lookup UI](https://royaltyregistry.xyz/lookup) to confirm your Engine contracts are correctly configured after completing the steps above.
