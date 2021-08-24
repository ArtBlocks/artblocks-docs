# Art Blocks 101 for Creators

## Documentation

The Art Blocks platform hosts generative projects for the production of verifiably deterministic outputs. A generative script (using [p5js](https://p5js.org/) for example) is stored immutably on the Ethereum blockchain for each project. When a user wants to purchase an iteration of a project hosted on the platform, they purchase an ERC721 compliant "non-fungible" token, also stored on the Ethereum blockchain, containing a provably unique "seed" which controls variables in the generative script. These variables, in turn, control the way the output looks and operates.

Each "seed", also known as a "hash string" is a hexadecimal string generated in a pseudo-random manner at the time the token is minted. Each character (0-9, a-f) represents a value from 0-15 and each pair of characters ("aa", or "f2") represents a value from 0-255.

For example:

```javascript
"0x11ac128f8b54949c12d04102cfc01960fc496813cbc3495bf77aeed738579738"
```

This hash will be the source of entropy or variation use to determine the output of your algorithm. When your art is rendered on Art Blocks, your script will have access to a global variable called `tokenData`. One of the first lines in your script should be to read in the hash from this variable.

```javascript
let hash = tokenData.hash
```

Included in the `tokenData` is also the `tokenId`. The `tokenId` encodes both the project and mint. 

`tokenId = (projectNumber * 1000000) + mintNumber`

If your script needs to know the mint number or project number, it can do so like this:

```javascript
let projectNumber = Math.floor(parseInt(tokenData.tokenId) / 1000000)
let mintNumber = parseInt(tokenData.tokenId) % (projectNumber * 1000000)
```

When you are testing locally, this variable obviously will not be defined in your browser environment. Thus here is a simple function to generate valid hashes and tokenIds.

```javascript
function random_hash() {
  let x = "0123456789abcdef", hash = '0x'
  for (let i = 64; i > 0; --i) {
    hash += x[Math.floor(Math.random()*x.length)]
  }
  return hash
}

tokenData = {
  "hash": random_hash(),
  "tokenId": "123000456"
}
```

There are two primary ways to use this hash:

### 1. Convert the hash to a large integer

The first method is to convert the hash into a large integer and use this to seed a pseudo random number generator (PRNGs). You want to consider PRNGs based on arithmetic to ensure your output is determistic regardless of the JavaScript version being used in a given browser. For example, do not use this to seed the `Math.random()` function because it's hard to say how this might change in the future.

```javascript
let seed = parseInt(tokenData.hash.slice(0, 16), 16)
```

Here is an example of a PRNG for demonstration purposes - please do your own research about PRNGs and choose one suitable for your needs. Disclaimer: "Anyone who considers arithmetical methods of producing random digits is, of course, in a state of sin." - [John von Neumann](https://en.wikipedia.org/wiki/John_von_Neumann).

#### Xorshift RNGs

George Marsaglia discovered Xorshift RNGs, proposing certain combinations of xorshift operations can result in sufficiently random number generators. For 32-bit inputs - there are many combinations (a, b, c) or triplets that could be used, one of which is **(5,17,13)**. For more information see the original publication below.

Source: Marsaglia, George. "Xorshift RNGs." Journal of Statistical Software, 8.14 (2003): 1 - 6. [10.18637/jss.v008.i14](https://www.jstatsoft.org/article/view/v008i14).  
Paper: [Creative Commons Attribution 3.0 Unported License](http://creativecommons.org/licenses/by/3.0/).     
Code: GNU General Public License (at least one of [version 2](http://www.gnu.org/licenses/gpl-2.0.html) or [version 3](http://www.gnu.org/licenses/gpl-3.0.html) or a [GPL-compatible license](https://gnu.org/licenses/license-list.html#GPLCompatibleLicenses).

Below is a modified shift-register generator derived from the concepts introduced by Marsaglia as well as a C-implementation of the Algorithm "xor" from p. 4 of Marsaglia, "Xorshift RNGs". 

```javascript
class Random {
  constructor(seed) {
    this.seed = seed
  }
  random_dec() {
    /* Algorithm "xor" from p. 4 of Marsaglia, "Xorshift RNGs" */
    this.seed ^= this.seed << 13
    this.seed ^= this.seed >> 17
    this.seed ^= this.seed << 5
    return ((this.seed < 0 ? ~this.seed + 1 : this.seed) % 1000) / 1000
  }
  random_num(a, b) {
    return a+(b-a)*this.random_dec()
  }
  random_int(a, b) {
    return Math.floor(this.random_num(a, b+1))
  }
}
```

Source: [https://en.wikipedia.org/wiki/Xorshift](https://en.wikipedia.org/wiki/Xorshift) licensed under [CC-BY-SA 3.0](https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License).

*Note: The code in this repository is purely for educational and demonstration purposes, please do your own research and testing before using any existing random number generators.*

We can seed it with our parsed hash string like so:

```javascript
let R = new Random(seed)
```

Now each time we need some randomness we can call various helper functions:

```javascript
R.random_dec()      // Random decimal (0-1)
R.random_num(0, 10) // Random decimal (0-10)
R.random_int(0, 10) // Random integer (0-10)
```

Every time one of these functions is called, `random_dec()` will also be called somewhere in the stack. Applying the determistic arithmetic to the seed and returning a new random number.

#### I heard I shouldn't use `Math.random()`. Why not?

When users mint each piece, they are creating a hash token on the blockchain. All the attributes of your piece should be derived from that token so that user will be able to render their piece and get the same results each time. `Math.random` is derived from the computer's clock, so even if it is seeded there is no guarantee you will get the same output on different computing environments in the future.

### 2. Create a series of hex pairs

Alternatively, you could just extract numbers from each of the hex pairs to parameterize your algorithm. Here we extract pairs and parse them into integers from 0-256. If we want them these values to range only between 0-10 for example we can do the following:

```javascript
let seed = parseInt(tokenData.hash.slice(0, 16), 16)
let p = []
for (let i = 0; i < 64; i+=2) {
  p.push(tokenData.hash.slice(i+2, i+4))
}
let rns = p.map(x => {return parseInt(x, 16) % 10})
```

These can be used to parameterize different variables later on:

```javascript
let border = rns[0] > 9
let size = rns[1] > 5 ? 10 : 20
let color = rns[2] > 7 ? "white" : "black"
```

## Guidelines and Constraints

Now you have the basics here are some general principles you need to consider when making your art. 

### Limited Dependencies
Each project can have zero or one library dependency. The approved dependencies are currently the following:

  + No Library at all (Vanilla JS, CSS, HTML, WebGL)
  + p5js(https://p5js.org/)
  + processing(https://processing.org/)
  + a-frame(https://aframe.io/)
  + threejs(https://threejs.org/)
  + vox
  + megavox
  + js
  + svg (https://svgjs.dev/)
  + custom
  + regl
  + tonejs

Additional libraries may be added at moderater discression, but the rule is only one external library per project.

### Deterministic
Each output must be determistic based on a single hash. More specifically, the initial output or frame must be the same. If your piece is animated, some randomness is okay. This is so when the art is rendered as an image (e.g. for OpenSea) it is always the same.

### Dimensionless
The output must be dimension agnostic. Meaning it scales seamlessly to any dimension. While you can control the dimension ratio (e.g. width/height can be 1.0, 1.5, 0.75 etc.) you have no control over the dimensions of the browser someone else might be using. The output will be rendered by the server at 2400x2400 (see below for ratios other than 1) and typically displayed in most browsers at 1000x1000 but your output should be the same at higher resolutions. Obviously, at lower resolutions, fewer pixels may limit what your output looks like, such as the smoothness of lines, which is okay. This is mainly to ensure your work can be reproduced at print quality.

A simple way to account for this is to define a default dimension and create a multiplier to scale coordinates or sizes relative to the canvas dimensions. Below uses p5js as an example but the same principle applies regardless of the language.

```javascript
var DEFAULT_SIZE = 1000
var WIDTH = window.innerWidth
var HEIGHT = window.innerHeight
var DIM = Math.min(WIDTH, HEIGHT)
var M = DIM / DEFAULT_SIZE

function setup() {
  createCanvas(WIDTH, HEIGHT)
  rect(100*M, 500*M, 50*M, 50*M)
}
```

Before submitting your script, it's probably a good idea to test it in different resolutions and aspect ratios.

Set the hash to a constant value:

```javascript
tokenData = {
	hash: "0x11ac16678959949c12d5410212301960fc496813cbc3495bf77aeed738579738", 
	tokenId: "123000456"
}
```

And then play with the browser window size, and refresh to check that your art looks the same at any resolution.

### Cost
Storing code on Ethereum is expensive! Taking average gas prices, you can generally expect to pay ~$10 for each full line of code your script requires. With that in mind - keep things efficient, maximize code reuse with functions, remove comments, and minify your finished code.


Based on previous projects, we've estimated the cost of uploading a script to be the following; where Bytes is the size of your project and gwei price is the price you set when submitting your transaction. It always helps to wait until non-peak hours to upload your script.

```
Cost (ETH) = 675 * Bytes * Gwei Price * (1/1000000000)
```

So a 10 KB project at 100 gwei would be:

```
675 * 10000 * 100 * (1 / 1000000000)
675000000 / 1000000000
0.675 ETH
```

Artists have recently targeted between ~5-20 KB for their code (without the library), but obviously this will vary by project scope. 

## Attribution

Much (generative art) source code is published under permissive copyleft licences, making it available to be used by everybody and depending on the license even for commercial purposes. In case your project's code contains any code not written by yourself, please inform the Art Blocks team about it so the appropriate considerations and attributions can be made.

Common source code licenses (in creative coding):

* [CC BY](https://creativecommons.org/licenses/by/4.0/): The original author and license must be clearly and appropriately stated.
* [CC BY-SA](https://creativecommons.org/licenses/by-sa/4.0/): As CC BY, but all derivates must also be licensed under CC BY-SA.
* [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/): As CC BY-SA, but no commercial use is allowed.
* [MIT](https://choosealicense.com/licenses/mit/): similar to CC BY
* [GPL](https://choosealicense.com/licenses/gpl-3.0/): similar to CC BY-SA

There are many other free-to-use licenses commonly used on open source software. Please carefully read the full details on any licensed code you re-use or modify, before including it in your project.

## Testing on Rinkeby

Once your script is ready, you will test it out on an [Art Blocks](https://rinkeby.artblocks.io/) clone site running on one of Ethereum's test networks (Rinkeby). This will make sure there aren't any bugs or errors and that if it's working on Rinkeby, it will work on Mainnet. You can connect to this site by changing the network in your browser wallet (e.g. the very top button of MetaMask). You'll still be using the same wallet and address, except on the test network.

Note: If you don't have "Rinkeby ETH" ask a mod or previous artist, we'll send you some to play with. Or if you don't feel like waiting, request some from the faucet: [https://faucet.rinkeby.io/](https://faucet.rinkeby.io/).

### Interacting with your Project
If you made it this far, we have probably requested a project name and an ethereum address from you. This is the address you will use on mainnet and on Rinkeby. So at this point change your network to Rinkeby in MetaMask. On Rinkeby, we'll practice uploading everything so that it all goes smooth on mainnet when the ETH is real. After loading the page and connecting your wallet, you should see a button labeled "Toggle Artist Interface". A multi-tabbed form will pop up. You only need to focused on the following:

#### Project
This should all be self-explanatory. Just fill and sumbit each one separately.

#### Token
In this tab you'll set the price and max invocations for your project. If you're accepting ETH as payment you don't need to worry about "Updated Currency Information". Although you can specify any ERC20-compliant token if you choose. Just give someone a heads up that you wish to go down this route.

#### Scripts
Here you'll first specify the dependency of your project including the script type and the version number *of that dependency*. For most scripts, you can leave the version blank or enter 1. The aspect ratio is a single number. E.g. 1 or 0.75 etc. If your piece takes a certain amount of time to fully render you can type in the animation length to let the server know when to render the canvas.

Once you've submitted your script details add your script to the "Project Script" box. Remember, `tokenData.hash` is a global variable in the environment this script will live in, so you do not need to define `tokenData` in your script, just expect your script will have access to it.

If your script is big, consider minifying it. If your script is so big that you cannot fit it in a single transaction (you're getting an error when you submit), you may need to split it up and submit each part subsequently.

#### URI

Set the baseURI depending on the network you are on. **Failure to do this will result in your images not rendering.** 

Rinkeby: `https://rinkebyapi.artblocks.io/token/`  

Mainnet: `https://api.artblocks.io/token/`

#### Finishing Actions
Once you're done let us know and we will activate the project. You can then click "Purchases Paused" to test out the minting. Once your test mints are working in the livescript view, mint 20-40.

#### How does my project get those OpenSea attributes?

Once your project is selected to be included in one of the Art Blocks collections, the onboarding team will help you with this. The one thing to keep in mind is that all of the attributes you want displayed should be directly generated from the transaction hash and should not depend on any other randomness. 

This script is essentially a copy of your rendering script but without any dependencies present (the server won't have access to them). It must define a variable called `features` in the outer most scope.

```
features = ["color: red", "shape: square"]
```

## Frequently Asked Questions

### Do I need to know solidity (the Ethereum scripting language)?

No. Art Blocks handles all of that for you. All you need to do is the artwork.

### Does the size include the library that I'm using?

No, the library you use is not stored on-chain with your project. A script tag linking to a CDN hosting the library you choose will be injected into the window scope when the project runs.

### Can I load external assets into my project (textures, audio, etc)?

Not yet. Some ideas are being worked on that will allow external assets to get pulled in, but currently everything must be included in the script file. For small and critical assets, you may be able to use `base-64` encoding to encode the asset into your script, but that will count as data to be stored.

### Can I use text? What fonts can I use?

You can use text in your project! Font choice is technically at your discression but you're encouraged to use the core web fonts to ensure universal support and maintain the integrity of the piece over the longer term. (`serif`, `sans-serif`, `monospace` and less commonly `cursive` and `fantasy`)
