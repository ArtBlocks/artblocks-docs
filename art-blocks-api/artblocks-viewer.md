# Artblocks Viewer
An overview of [live.artblocks.io](https://live.artblocks.io/)

## Routes
>All routes are for the environment specified in .env file and act as such. i.e. Ropsten contracts will not work on mainnet and vice versa

**live.artblocks.io/**
Home page of the site which returns the latest *rendered* minted token from any of the Art Blocks contracts  

**live.artblocks.io/`{CONTRACT_ADDRESS}`** enter any Art Blocks or PBAB contract and you be presented with the latest *rendered* mint.  
+ *Example:* [Latest Artblocks_VO mint](https://live.artblocks.io/0x059edd72cd353df5106d2b9cc5ab83a52287ac3a)

**live.artblocks.io/`{CONTRACT_ADDRESS}`/`{PROJECT_INDEX}`** enter any Art Blocks or PBAB contract followed by the index of the project and you be presented with the latest *rendered* mint.   
+ *Example:* [Latest Chromie Squiggle mint](https://live.artblocks.io/0x059edd72cd353df5106d2b9cc5ab83a52287ac3a/0)

**live.artblocks.io/token/`{TOKEN_ID}`** enter any Art Blocks or PBAB token id and you are presented with that token.   
+ *Example:* [Chromie Squiggle mint #71](https://live.artblocks.io/token/0x059edd72cd353df5106d2b9cc5ab83a52287ac3a-71)

## Contracts
This is a running list of contract addresses for various Art Blocks and PBAB

**Mainnet**:
+ Artblocks_VO: 0x059edd72cd353df5106d2b9cc5ab83a52287ac3a
+ Artblocks_V1: 0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270
+ ARTCODE: 0xd10e3dee203579fcee90ed7d0bdd8086f7e53beb
+ Doodle Labs: 0x28f2d3805652fb5d359486dffb7d08320d403240
+ CryptoCitizens: 0xbdde08bd57e5c9fd563ee7ac61618cb2ecdc0ce0
+ Flutter: 0x13aae6f9599880edbb7d144bb13f1212cee99533
+ MOMENT: 0x0a1bbd57033f57e7b6743621b79fcb9eb2ce3676
+ Plottables: 0xa319c382a702682129fcbf55d514e61a16f97f9c
+ TBOA: 0x62e37f664b5945629b6549a87f8e10ed0b6d923b

## Customizable Display
You can create a customizable display for any route on artblocks-viewer. This is done through query params added to the end of the url. In order to activate this ability you must first add `?useCustomViewParams=true` to the end of the whatever route you are using. [Here](https://live.artblocks.io/token/0x059edd72cd353df5106d2b9cc5ab83a52287ac3a-71?useCustomViewParams=true) is the most basic customized url of Chromie Squiggle mint #71 with just the squiggle centered in the middle of the page.

All of the customization that can be done and the default values are as follows:

- **useCusomtomViewParams**: this is to specify you are using the custom view display and all other params require this to be true. `default: false`
- **width**: this can be any valid html size and is the width of the token being displayed `default: 90vw`
- **height**: this can be any valid html size and is the height of the token being displayed `default: 90vh`
- **backgroundColor**: this can be any six digit hex color and is the background color of the page `default: ffffff`
- **showText**: this is whether or not to show the text information about the currently displayed token. All other text params depend on this to be true to work `default: false`
- **textColor**: this can be any six digit hex color and is the color of the text `default: 000000`
- **fontSize**: this can be any valid html size and is the size of the text `default: 20px`
- **textBackground**: this can be any six digit hex color and is the background color of the text `default: none`
- **textBottom**: this can be any valid html size and is the distance from the bottom of the screen of the text `default: 3em`

**Example URLs**:
- [Latest Chimera](https://live.artblocks.io/0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270/233?useCustomViewParams=true&backgroundColor=F8C8DC&showText=true)
- [Latest Artblocks Mint](https://live.artblocks.io/0xa7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd270/?useCustomViewParams=true&backgroundColor=a2beb1&showText=true&textBackground=000000&fontSize=30px&textColor=ffffff&textBottom=1em)
- [Streamlines #414](https://live.artblocks.io/token/0xa319c382a702682129fcbf55d514e61a16f97f9c-414/?useCustomViewParams=true&backgroundColor=671108&showText=true&textColor=bfb3b2&textBottom=0.5em&width=425px&height=550px)

