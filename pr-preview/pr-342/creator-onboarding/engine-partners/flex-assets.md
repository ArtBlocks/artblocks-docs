# Decentralized Storage Assets

Art Blocks Engine Flex supports several types of external dependencies — including PostParams (on-chain), multiple Dependency Registry entries, and decentralized storage networks. This page covers the decentralized storage path: how to upload assets to IPFS using Pinata or Filebase, and how to reference them in your generative script.

---

## When to Use Decentralized Storage

Engine Flex supports many use cases beyond decentralized storage — see [What is Art Blocks Engine?](/creator-onboarding/engine-partners/what-is-engine/) for the full picture. This page focuses specifically on the IPFS and Arweave storage path, which is useful when your project incorporates assets too large to store efficiently on-chain:

- **Images** — base images for generative manipulation (1-of-1-of-X outputs)
- **Audio** — generative audio composed from uploaded samples
- **ML models** — machine learning models (e.g. TensorFlow.js models)
- **Large data sets** — any structured data used as generative input

Your generative script still lives fully on-chain. External assets are referenced by CID (content identifier) and loaded at render time via the preferred gateway.

---

## Accessing Flex Assets in Your Script

External assets are injected into `tokenData.externalAssetDependencies`. Access them like this:

```javascript
const dep = tokenData.externalAssetDependencies[0]; // first external dependency

if (dep.dependency_type === "IPFS") {
  const url = tokenData.preferredIPFSGateway + dep.cid;
  // fetch or load the asset from `url`
} else if (dep.dependency_type === "ARWEAVE") {
  const url = tokenData.preferredArweaveGateway + dep.cid;
  // fetch or load the asset from `url`
} else if (dep.dependency_type === "ONCHAIN") {
  const data = dep.data; // already resolved on-chain data string
}
```

For projects with multiple external assets:

```javascript
const assets = tokenData.externalAssetDependencies;
// e.g. assets[0] is the base image, assets[1] is an audio sample
```

---

## Uploading to IPFS with Pinata

[Pinata](https://www.pinata.cloud/) is an IPFS pinning service designed for creators and non-technical users.

### Sign Up

Visit [pinata.cloud](https://www.pinata.cloud/) and click **Sign Up**. The free plan supports up to 100 files and 1 GB of storage.

### Upload a File

1. After signing in, you'll see your Files page
2. Click **Upload +** → **File**
3. Click **Select File** and choose your file
4. Give it a name and click **Upload**

Once uploaded, the file appears in your Files list with a **CID** (Content Identifier) — this is the key value you'll use in your Art Blocks project configuration. A CID looks like:

```
QmNrCnsNazd54aAQixQCVtikJNfizEXGKR6yLhr9P1TTJV
```

### Preview Your File

Click the file name to preview it in a new window using the Pinata gateway:

```
https://gateway.pinata.cloud/ipfs/<CID>
```

!!!info
The default Pinata gateway is suitable for testing only. For production, consider a [Dedicated Gateway](https://www.pinata.cloud/blog/the-power-of-dedicated-gateways) on a paid plan.
!!!

For questions, visit [Pinata's docs](https://docs.pinata.cloud) or email [team@pinata.cloud](mailto:team@pinata.cloud).

---

## Uploading to IPFS with Filebase

[Filebase](https://filebase.com/) is a geo-redundant IPFS pinning service with 3x geographic redundancy — each uploaded file is pinned to 3 IPFS nodes across different regions.

### Sign Up

Visit [filebase.com](https://filebase.com/) and click **Try for Free**. The free tier supports up to 5 GB and 1,000 files with no credit card required.

1. Fill in the sign-up form (email, password)
2. Confirm your email by clicking the link in the confirmation email

### Upload a File

1. Sign in to the [Filebase console](https://console.filebase.com)
2. Select **Buckets** from the left menu → **Create Bucket**
3. Give your bucket a name and select **IPFS** for the network
4. Open your bucket and click **Upload**
5. Select a file, folder, or existing IPFS CID
6. After upload, your file will appear with an IPFS CID value

The CID is what you use in your Art Blocks script. Preview your file at:

```
https://ipfs.filebase.io/ipfs/<CID>
```

For increased performance and custom configuration, Filebase offers [Dedicated Gateways](https://docs.filebase.com/ipfs/ipfs-gateways/getting-started-with-ipfs-dedicated-gateways) on paid plans.

For questions, visit [Filebase's docs](https://docs.filebase.com) or email [hello@filebase.com](mailto:hello@filebase.com).

---

## Configuring Flex Assets in the Creator Dashboard

Once you have your CIDs, configure your external asset dependencies in the Art Blocks Creator Dashboard:

1. Navigate to your project → **Scripts**
2. In the **Flex Assets** section, add your dependencies
3. For each dependency, specify:
   - **Dependency Type**: IPFS, ARWEAVE, or ONCHAIN
   - **CID**: Your content identifier
4. The order of dependencies corresponds to indices in `tokenData.externalAssetDependencies`

---

## Setting the Preferred Gateway

Each Engine Flex contract has a configured preferred IPFS gateway and preferred Arweave gateway. These values are injected into `tokenData` and your script should use them to construct asset URLs:

```javascript
// Construct IPFS URL using preferred gateway
const ipfsUrl = tokenData.preferredIPFSGateway + dep.cid;

// Construct Arweave URL using preferred gateway
const arweaveUrl = tokenData.preferredArweaveGateway + dep.cid;
```

The preferred gateways are configured at the contract level by the Engine admin. Contact the Art Blocks team if you need to update your contract's preferred gateways.

---

## Arweave

For permanent, pay-once storage, Arweave is an excellent option. Files on Arweave are permanently stored on the Arweave blockchain.

Popular Arweave upload tools:
- [Ardrive](https://ardrive.io/) — web interface for uploading to Arweave
- [Bundlr (now Irys)](https://irys.xyz/) — programmatic uploads with various payment options

After uploading, you'll receive a transaction ID. Use this as the CID in your Flex asset configuration with `ARWEAVE` dependency type.

---

## Asset Size Limits

There is no strict size limit for external assets, but consider:

- **Larger assets** take longer to load at render time, affecting user experience
- **IPFS** performance depends on gateway availability and pinning redundancy
- **Arweave** files are permanent but retrieval speed varies by gateway

Test your project with realistic network conditions to ensure assets load within your render delay window.
