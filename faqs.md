---
description: Frequently asked questions.
---

# FAQs

## Do I need to know Solidity \(to write my own smart contracts\)?

No. Art Blocks handles all of that for you. All you need to do is the artwork.

## Does the size include the library that I'm using?

No, the library you use is not stored on-chain with your project. A script tag linking to a CDN hosting the library you choose will be injected into the window scope when the project runs.

## Can I load external assets into my project \(textures, audio, etc\)?

Not yet. Some ideas are being worked on that will allow external assets to get pulled in, but currently everything must be included in the script file. For small and critical assets, you may be able to use `base-64` encoding to encode the asset into your script, but that will count as data to be stored.

## Can I use text? What fonts can I use?

You can use text in your project! Font choice is technically at your discretion but you're encouraged to use the core web fonts to ensure universal support and maintain the integrity of the piece over the longer term. \(`serif`, `sans-serif`, `monospace` and less commonly `cursive` and `fantasy`\)



