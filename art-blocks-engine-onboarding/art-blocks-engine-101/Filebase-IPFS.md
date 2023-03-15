---
order: 290
---

# Using Filebase for External Assets

Filebase is a geo-redundant IPFS pinning service and decentralized storage provider. When a file is uploaded to an IPFS bucket on Filebase, it is automatically pinned to the IPFS network with 3 duplicate copies, each of which is stored on an IPFS node located across 3 unique, geographic regions.

Filebase offers an easy-to-use Web Console Dashboard for non-technical users, and an S3-compatible API for developers to utilize in a wide variety of tool configurations or SDKs. 

## Signing Up

Filebase uses a web-based console that can be found at https://filebase.com/signup. Existing accounts can go directly to https://console.filebase.com.

To sign up for a Filebase account, navigate to https://filebase.com. To make a new account, click the ‘Try for Free’ button in the top right corner of the webpage. ![signup](/static/Filebase_setup1.png)

Filebase is a free-to-use platform for all users. All users can store up to 5GB of data, with a maximum of 1,000 individual files on the IPFS network with no credit card required. 

Next, fill out the fields of the form, including an email address and password, and agree to the Filebase terms to create your account. 

You will receive an email with confirmation instructions. Click the link included in the email to confirm your account and finish the registration process. 
Once you’ve completed these steps, your Filebase account has been created. 

## Uploading Content
Once signed in, you will be brought to the Filebase dashboard. ![web_dashboard](/static/Filebase_setup2.png)

To upload content, first you will need an IPFS bucket. Select 'Buckets' from the left menu bar, then select 'Create Bucket'. ![buckets](/static/Filebase_setup3.png)

Give your bucket a name, then select IPFS for the network. ![bucket_ipfs](/static/Filebase_setup4.png)

Then, select your bucket from the Buckets menu and select 'Upload'. You can choose to upload a File, Folder, or existing IPFS CID to Filebase. For this example, we'll use a single file. ![upload](/static/Filebase_setup5.png)

You will be prompted to select a file from your computer. Once uploaded, it'll be displayed in the Filebase web console and it will be given an IPFS CID value. ![cid](/static/Filebase_setup6.png)

When a file is uploaded to IPFS, the file’s contents are used to generate a cryptographic hash value. Then, this hash value is used to generate another value, which is used as the file’s content identifier (CID). CIDs are used to access files stored on IPFS, but instead of locating the file on the network based on it's name, the CID is based on the file's contents. Any changes to the file's contents or metadata will result in a new, unique CID.

The CID value is what is used within an Art Blocks generative script, under the 'CID' field. 

To preview your file using it's IPFS CID and the Filebase public gateway, you can use the following URL format in any web browser:

https://ipfs.filebase.io/ipfs/[CID]

The Filebase public IPFS gateway is [https://ipfs.filebase.io/ipfs](https://ipfs.filebase.io/ipfs) and can be used by all Filebase uses to host Filebase pinned CIDs. For increased configuration options, performance, content whitelisting, and custom branding, a Filebase [Dedicated Gateway](https://docs.filebase.com/ipfs/ipfs-gateways/getting-started-with-ipfs-dedicated-gateways) can be used through one of Filebase's [paid IPFS plans.](https://docs.filebase.com/getting-started/billing-and-pricing/pricing-model#subscription-tiers) 

For more information, visit Filebase's extensive [documentation](https://docs.filebase.com) or send them an email at [hello@filebase.com](hello@filebase.com)! or reach out directly to the Art Blocks team. 
