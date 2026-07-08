---
order: 850
description: How to define IPFS and Arweave CIDs and preferred gateway URLs for Art Blocks Engine Flex projects, with concrete examples.
---

# Decentralized Storage Assets (IPFS & Arweave)

Art Blocks Engine Flex supports several types of external dependencies — including PostParams (on-chain), multiple Dependency Registry entries, and decentralized storage networks. This page covers the decentralized storage path: what a CID is, how preferred gateway URLs are constructed, how to upload assets to IPFS or Arweave, and how to reference them in your generative script.

!!!info
Decentralized storage assets are an **Engine Flex** feature. If you're building a standard Art Blocks Flagship or standard Engine project, your script and dependencies are fully on-chain and this page doesn't apply to you.
!!!

---

## When to Use Decentralized Storage

Engine Flex supports many use cases beyond decentralized storage — see [What is Art Blocks Engine?](/creator-onboarding/engine-partners/what-is-engine/) for the full picture. This page focuses specifically on the IPFS and Arweave storage path, which is useful when your project incorporates assets too large to store efficiently on-chain:

- **Images** — base images for generative manipulation (1-of-1-of-X outputs)
- **Audio** — generative audio composed from uploaded samples
- **ML models** — machine learning models (e.g. TensorFlow.js models)
- **Large data sets** — any structured data used as generative input

Your generative script still lives fully on-chain. External assets are referenced by **CID** (content identifier) and loaded at render time via the **preferred gateway**.

---

## CIDs and Gateways in Practice

A **CID** is just an identifier for a piece of content on a decentralized network — it doesn't include a protocol, domain, or path. To actually fetch the content over HTTP, you need to combine it with a **gateway URL**: a web server that knows how to translate a CID into the underlying content.

```
finalURL = gatewayURL + CID
```

That's the entire mental model. Everything else on this page is detail around getting the CID and gateway values right.

### IPFS CIDs

IPFS CIDs come in two formats, and you may encounter either depending on which tool generated it:

| Format | Example | Notes |
|---|---|---|
| **CIDv0** | `QmbxU6subfSzzpxketBhVBVCGhFBPdTSB8nCtppGZtpZGf` | Starts with `Qm`, base58-encoded. Most common with legacy tools. |
| **CIDv1** | `bafybeigdyrzt5sfp7udm7hu76uh7y26nf3efuylqabf3oclgtqy55fbzdi` | Starts with `ba`, base32-encoded. Increasingly the default in newer tools (e.g. Pinata, Filebase). |

Both formats work identically as far as Art Blocks and IPFS gateways are concerned — use whichever your upload tool gives you, and paste it verbatim into the **CID** field in the Creator Dashboard.

### Arweave CIDs (Transaction IDs)

Arweave doesn't use the term "CID," but the Art Blocks Creator Dashboard uses the same **CID** field for Arweave dependencies. For Arweave, the value you enter is the **transaction ID** returned after your upload completes:

```
DKm4z1RwyMnhSs9dHkQPqUw4wXAqjEuNsCr1ScYoOZM
```

Arweave transaction IDs are always 43 characters, base64url-encoded (letters, numbers, `-`, and `_`).

### Preferred Gateway URLs

A gateway URL is the prefix that, when concatenated with a CID, produces a working link to the content. Every gateway has its own URL shape — the important thing is that the gateway value stored on your contract already includes any trailing slash or path segment needed, so that simple string concatenation with the CID produces a valid URL.

| Network | Example preferred gateway | Example CID | Resulting URL |
|---|---|---|---|
| IPFS | `https://ipfs.artblocks.io/ipfs/` | `QmbxU6subfSzzpxketBhVBVCGhFBPdTSB8nCtppGZtpZGf` | `https://ipfs.artblocks.io/ipfs/QmbxU6subfSzzpxketBhVBVCGhFBPdTSB8nCtppGZtpZGf` |
| IPFS (Pinata dedicated) | `https://designator-string.mypinata.cloud/ipfs/` | `bafybeigdyrzt5sfp7udm7hu76uh7y26nf3efuylqabf3oclgtqy55fbzdi` | `https://designator-string.mypinata.cloud/ipfs/bafybeigdyrzt5sfp7udm7hu76uh7y26nf3efuylqabf3oclgtqy55fbzdi` |
| Arweave | `https://arweave.net/` | `DKm4z1RwyMnhSs9dHkQPqUw4wXAqjEuNsCr1ScYoOZM` | `https://arweave.net/DKm4z1RwyMnhSs9dHkQPqUw4wXAqjEuNsCr1ScYoOZM` |

!!!warning
Watch the trailing slash. `https://arweave.net` (no slash) concatenated with a transaction ID produces a broken URL like `https://arweave.netDKm4...`. Always confirm the gateway value ends in `/` (or otherwise ends exactly where the CID should begin) before it's set on your contract.
!!!

The preferred gateways are configured **at the contract level** by the Engine admin — not per-project or per-asset. Every project on a given Engine Flex contract shares the same preferred IPFS and Arweave gateways. If you're an artist and need a gateway changed, contact your Engine partner or the Art Blocks team; if you're an Engine partner, see the [Engine Partner FAQ](/creator-onboarding/engine-partners/faq/#technical) for how to request a change.

---

## Accessing Flex Assets in Your Script

External assets are injected into `tokenData.externalAssetDependencies`, alongside `tokenData.preferredIPFSGateway` and `tokenData.preferredArweaveGateway`. Access them like this:

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

## Concrete End-to-End Example

Here's a full walkthrough of a project with one IPFS image dependency, from Creator Dashboard configuration to a resolved fetch in the browser.

**1. You configure a Flex Asset in the Creator Dashboard:**

| Field | Value |
|---|---|
| Dependency Type | `IPFS` |
| CID | `QmbxU6subfSzzpxketBhVBVCGhFBPdTSB8nCtppGZtpZGf` |

**2. Your Engine Flex contract has a preferred IPFS gateway configured at the contract level:**

```
https://ipfs.artblocks.io/ipfs/
```

**3. At render time, the Generator injects the following into `tokenData`:**

```javascript
let tokenData = {
  hash: "0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef",
  tokenId: "42000001",
  preferredIPFSGateway: "https://ipfs.artblocks.io/ipfs/",
  preferredArweaveGateway: "https://arweave.net/",
  externalAssetDependencies: [
    {
      dependency_type: "IPFS",
      cid: "QmbxU6subfSzzpxketBhVBVCGhFBPdTSB8nCtppGZtpZGf",
      data: null,
    },
  ],
};
```

**4. Your script constructs the final URL and loads the asset:**

```javascript
const dep = tokenData.externalAssetDependencies[0];
const imageUrl = tokenData.preferredIPFSGateway + dep.cid;
// imageUrl === "https://ipfs.artblocks.io/ipfs/QmbxU6subfSzzpxketBhVBVCGhFBPdTSB8nCtppGZtpZGf"

let baseImg;
function preload() {
  baseImg = loadImage(imageUrl);
}
```

The same pattern applies to an Arweave dependency — swap `dependency_type: "ARWEAVE"`, use `dep.cid` as the transaction ID, and read from `tokenData.preferredArweaveGateway` instead.

---

## Uploading Your Assets

You'll need to pin your file to IPFS or upload it to Arweave before you have a CID to configure. A few popular options:

- **[Pinata](https://www.pinata.cloud/)** — IPFS pinning with a simple upload UI. Free plan covers up to 100 files / 1 GB. After upload, the file's CID is shown in your Files list.
- **[Filebase](https://filebase.com/)** — IPFS pinning with 3x geo-redundant nodes. Free tier covers up to 5 GB / 1,000 files.
- **[Ardrive](https://ardrive.io/)** or **[Irys](https://irys.xyz/)** — for permanent, pay-once storage on Arweave. After upload, you'll receive a transaction ID to use as your CID.

Each service's dashboard shows the resulting CID (or transaction ID) directly after upload — copy it into the Creator Dashboard as described below. For production projects, consider a dedicated/custom gateway (offered by Pinata and Filebase) rather than the shared public gateway, which is best suited for testing.

---

## Configuring Flex Assets in the Creator Dashboard

Once you have your CIDs, configure your external asset dependencies in the Art Blocks Creator Dashboard:

1. Navigate to your project → **Scripts**
2. In the **Flex Assets** section, add your dependencies
3. For each dependency, specify a **Dependency Type** (IPFS, ARWEAVE, or ONCHAIN) and its **CID**
4. The order of dependencies corresponds to indices in `tokenData.externalAssetDependencies`

Larger assets take longer to load at render time, so test with realistic network conditions to ensure assets load within your render delay window.

---

## For Engine Partners

The examples above cover the artist/script side of IPFS and Arweave assets. If you're an Engine partner responsible for configuring or updating the **preferred gateway** at the contract level, see the [Engine Partner FAQ](/creator-onboarding/engine-partners/faq/#technical) and [What is Art Blocks Engine?](/creator-onboarding/engine-partners/what-is-engine/#engine-flex-capabilities) for the partner-facing side of this feature.
