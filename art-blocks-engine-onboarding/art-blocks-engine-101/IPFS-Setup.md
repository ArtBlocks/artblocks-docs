---
order: 300
---

# Using Pinata for External Assets

Pinata is an excellent IPFS resource built with creators and non-technical users in mind, making it easy to upload content that you can use inside Art Blocks! This will walk you through the basics of uploading content to Pinata. 

## Signing Up

You can sign up for a free account which will allow up to 100 files and 1GB of storage! To get started visit [pinata.cloud](https://bit.ly/3DtEmhN) and click the “Sign Up” button in the top right. It will ask you for a name, email, and password. 

## Uploading Content
Once you’re signed in you will see the Files Page which looks something like this: ![setup](/static/Pinata_setup_1.png)


To start uploading content, simply click on the “Upload +” button and select “File” ![upload](/static/Pinata_setup_2.png)


Of course from there click “Select File” and choose the file on your computer ![select](/static/Pinata_setup_3.png)


Then give it a name, and click upload; that’s it! ![name](/static/Pinata_setup_4.png)


Once it’s done uploading you will see the file listed on your files page! ![complete](/static/Pinata_setup_5.png)

What’s important to note is the “CID” which stands for “Content Identifier.” It’s the core of IPFS and how files can be shared across the IPFS network. This is what you would input into the “cid” portion of an Art Blocks generative script and would look something like this: 

QmNrCnsNazd54aAQixQCVtikJNfizEXGKR6yLhr9P1TTJV

If you want to preview your file you can simply click on the name of the file on the left side and it will open a preview in a new window.

The default Pinata gateway is [https://gateway.pinata.cloud](https://gateway.pinata.cloud) but keep in mind that it should only be used for testing files. For production work you may want to consider getting a [Dedicated Gateway](https://www.pinata.cloud/blog/the-power-of-dedicated-gateways) on a paid plan. 

If you have further questions be sure to visit Pinata's [docs](https://docs.pinata.cloud) and do not hesitate to send them an email at [team@pinata.cloud](team@pinata.cloud)! or reach out directly to the Art Blocks team. 
