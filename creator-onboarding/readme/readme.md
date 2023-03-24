# Art Blocks 101 for Creators

A guide on getting started as a creator with Art Blocks.

!!!
**The primary audience for this document is artists who have already entered the pipeline for launching a project on Art Blocks. If you are an artist currently waiting in the applications queue or applying to Art Blocks, this documentation will provide a helpful guide for you in terms of what to expect, but many of the steps here will not be actionable for you until you have had a project shell set up by the Art Blocks team.**
!!!

!!!
**Artists will likely need to tweak/optimize their project code to get it working in the Art Blocks environment.** Specifically, static images are rendered for all projects (used as thumbnails, on other platforms, etc.). To generate these, Art Blocks currently uses compute instances running headless Chromium with [Puppeteer](https://github.com/puppeteer/puppeteer). Headless Chromium requires the use of [SwiftShader](https://swiftshader.googlesource.com/SwiftShader/+/HEAD/docs/Index.md), a CPU implementation of the GPU API. This means GPU intensive projects will render slower and may require code optimization and performance improvements from the artist. To closely replicate this environment on your end while developing, we recommend using Chrome and turning **off** "Use Hardware Acceleration" in Settings.
!!!

## Documentation

The Art Blocks platform hosts generative projects for the production of verifiably deterministic outputs. A generative script (using [p5js](https://p5js.org) for example) is stored immutably on the Ethereum blockchain for each project. When a user wants to purchase an iteration of a project hosted on the platform, they purchase an ERC721 compliant "non-fungible" token, also stored on the Ethereum blockchain, containing a provably unique "seed" which controls variables in the generative script. These variables, in turn, control the way the output looks and operates.

Each "seed", also known as a "hash string" is a hexadecimal string generated in a pseudo-random manner at the time the token is minted. Each character (0-9, a-f) represents a value from 0-15 and each pair of characters ("aa", or "f2") represents a value from 0-255.

For example:

```js
"0x11ac128f8b54949c12d04102cfc01960fc496813cbc3495bf77aeed738579738";
```

This hash will be the source of entropy or variation use to determine the output of your algorithm. When your art is rendered on Art Blocks, your script will have access to a global variable called `tokenData`. One of the first lines in your script should be to read in the hash from this variable.

```js
let hash = tokenData.hash;
```

Included in the `tokenData` is also the `tokenId`. The `tokenId` encodes both the project and mint.

**Please note:** if you include using the `tokenId` as a way to determine the outputs of your script **you must** disclose this as part of the release communications for your project.

```
tokenId = (projectNumber * 1000000) + mintNumber
```

If your script needs to know the mint number or project number, it can do so like this:

```js
let projectNumber = Math.floor(parseInt(tokenData.tokenId) / 1000000);
let mintNumber = parseInt(tokenData.tokenId) % 1000000;
```

When you are testing locally, this variable obviously will not be defined in your browser environment. This here is a simple function to generate valid hashes and tokenIds.

```js
function genTokenData(projectNum) {
  let data = {};
  let hash = "0x";
  for (var i = 0; i < 64; i++) {
    hash += Math.floor(Math.random() * 16).toString(16);
  }
  data.hash = hash;
  data.tokenId = (
    projectNum * 1000000 +
    Math.floor(Math.random() * 1000)
  ).toString();
  return data;
}
let tokenData = genTokenData(123);
```

### Safely deriving randomness from the token hash

Art Blocks requires that all artists use an instance of the following Random class to feed all of their project's randomness. If you need to modify/customize the Random class, please flag this to our team during the review process.

```js
class Random {
  constructor() {
    this.useA = false;
    let sfc32 = function (uint128Hex) {
      let a = parseInt(uint128Hex.substring(0, 8), 16);
      let b = parseInt(uint128Hex.substring(8, 16), 16);
      let c = parseInt(uint128Hex.substring(16, 24), 16);
      let d = parseInt(uint128Hex.substring(24, 32), 16);
      return function () {
        a |= 0;
        b |= 0;
        c |= 0;
        d |= 0;
        let t = (((a + b) | 0) + d) | 0;
        d = (d + 1) | 0;
        a = b ^ (b >>> 9);
        b = (c + (c << 3)) | 0;
        c = (c << 21) | (c >>> 11);
        c = (c + t) | 0;
        return (t >>> 0) / 4294967296;
      };
    };
    // seed prngA with first half of tokenData.hash
    this.prngA = new sfc32(tokenData.hash.substring(2, 34));
    // seed prngB with second half of tokenData.hash
    this.prngB = new sfc32(tokenData.hash.substring(34, 66));
    for (let i = 0; i < 1e6; i += 2) {
      this.prngA();
      this.prngB();
    }
  }
  // random number between 0 (inclusive) and 1 (exclusive)
  random_dec() {
    this.useA = !this.useA;
    return this.useA ? this.prngA() : this.prngB();
  }
  // random number between a (inclusive) and b (exclusive)
  random_num(a, b) {
    return a + (b - a) * this.random_dec();
  }
  // random integer between a (inclusive) and b (inclusive)
  // requires a < b for proper probability distribution
  random_int(a, b) {
    return Math.floor(this.random_num(a, b + 1));
  }
  // random boolean with p as percent liklihood of true
  random_bool(p) {
    return this.random_dec() < p;
  }
  // random value in an array of items
  random_choice(list) {
    return list[this.random_int(0, list.length - 1)];
  }
}
```

_Note that the class uses the prng algorithm sfc32, which was designed and coded by_ [_Chris Doty-Humphry and is public domain_](http://pracrand.sourceforge.net/license.txt)_. More information can be found at_ [_http://pracrand.sourceforge.net_](http://pracrand.sourceforge.net)_._

The convenience methods `random_num`, `random_int`, `random_bool`, and `random_choice` may be removed if not needed for a specific project. Artists may also add their own convenience methods, but all randomness should be originally sourced from the `random_dec()` function.

We can get an instance of the Random class like so:

```js
let R = new Random();
```

Now each time we need some randomness we can call various helper functions:

```js
R.random_dec(); // Random decimal [0-1)
R.random_num(0, 10); // Random decimal [0-10)
R.random_int(0, 10); // Random integer [0-10]
R.random_bool(0.5); // Random boolean with probability 0.5
R.random_choice([1, 2, 3]); // Random choice from a given list. Great for getting a random color from a discrete color palette
```

Every time one of these functions is called, `random_dec()` will also be called somewhere in the stack, applying the deterministic arithmetic to the seed and returning a new random number.

#### I heard I shouldn't use `Math.random()`. Why not?

When users mint each piece, they are creating a hash token on the blockchain. All the attributes of your piece should be derived from that token so that user will be able to render their piece and get the same results each time. `Math.random` is derived from the computer's clock, so there is no guarantee you will get the same output on different computing environments in the future.

## Guidelines and Constraints

Now you have the basics here are some general principles you need to consider when making your art.

### Limited Dependencies

Each project can have zero or one library dependency. The approved dependencies are currently the following:

| Library           | Version       | Source                             | Notes                                                 |
| ----------------- | ------------- | ---------------------------------- | ----------------------------------------------------- |
| No Library at all |               | Vanilla JS, CSS, HTML, WebGL       |
| svg               |               |
| p5.js             | `v1.0.0`      | https://p5js.org                   |
| processing.js     | `v1.4.6`      | https://processing.org             |
| a-frame           | `v1.2.0`      | https://aframe.io                  |
| three.js          | `r124`        | https://threejs.org                |
| babylon.js        | `v5.0.0`      | https://babylonjs.com              | Canvas element provided by template (#babylon-canvas) |
| vox               | `v1.1.0-beta` |
| megavox           | `v1.1.0-beta` |
| regl              | `v2.1.0`      |
| tone.js           | `v14.8.15`    | https://tonejs.github.io           |
| twemoji           | `v14.0.2`     | https://github.com/twitter/twemoji |
| paper.js          | `v0.12.15`    | http://paperjs.org                 |
| Zdog              | `v1.1.2`      | https://github.com/metafizzy/zdog  |

Additional libraries may be added at moderator discretion, but the rule is only one external library per project.

### Code templates by dependency type

When uploading your project to testnet, you may refer to this script template: https://github.com/ArtBlocks/node-artblocks/blob/main/src/templates.js

### Deterministic

Each output must be deterministic based on a single hash. More specifically, the initial output or frame must be the same. If your piece is animated, some randomness is okay. This is so when the art is rendered as an image (e.g. for OpenSea) it is always the same.

### Dimensionless

The output must be dimension agnostic. Meaning it scales seamlessly to any dimension. While you can control the dimension ratio (e.g. width/height can be 1.0, 1.5, 0.75 etc.) you have no control over the dimensions of the browser someone else might be using. The output will be rendered by the server at 2400x2400 (see below for ratios other than 1) and typically displayed in most browsers at 1000x1000 but your output should be the same at higher resolutions. Obviously, at lower resolutions, fewer pixels may limit what your output looks like, such as the smoothness of lines, which is okay. This is mainly to ensure your work can be reproduced at print quality.

A simple way to account for this is to define a default dimension and create a multiplier to scale coordinates or sizes relative to the canvas dimensions. Below uses p5js as an example but the same principle applies regardless of the language.

```js
var DEFAULT_SIZE = 1000;
var WIDTH = window.innerWidth;
var HEIGHT = window.innerHeight;
var DIM = Math.min(WIDTH, HEIGHT);
var M = DIM / DEFAULT_SIZE;

function setup() {
  createCanvas(WIDTH, HEIGHT);
  rect(100 * M, 500 * M, 50 * M, 50 * M);
}
```

Before submitting your script, it's probably a good idea to test it in different resolutions and aspect ratios.

Set the hash to a constant value:

```js
tokenData = {
  hash: "0x11ac16678959949c12d5410212301960fc496813cbc3495bf77aeed738579738",
  tokenId: "123000456",
};
```

And then play with the browser window size, and refresh to check that your art looks the same at any resolution.

### Shaders

If you are using shaders, you must include the shader code in the script itself (not in a separate file). A typical vertex & fragment shader might be defined like the following:

```js
const vertexShader = `
  // Vertex shader code
  attribute vec2 aTexCoord;
  ...
`;
const fragmentShader = `
  // Fragment shader code
  varying vec2 vTexCoord;
  ...
`;
```

These can then be used by the library you are using to render your art. For example, if using p5js:

```js
let shaderProgram;
function setup() {
  createCanvas(100, 100, WEBGL);
  shaderProgram = createShader(vertexShader, fragmentShader);
  shader(shaderProgram);
}
```

### Cost

Storing code on Ethereum is expensive! Taking average gas prices, you can generally expect to pay \~$10 for each full line of code your script requires. With that in mind - keep things efficient, maximize code reuse with functions, remove comments, and minify your finished code.

Based on previous projects, we've estimated the cost of uploading a script to be the following; where Bytes is the size of your project and gwei price is the price you set when submitting your transaction. It always helps to wait until non-peak hours to upload your script.

```
Cost (ETH) = 235 * Bytes * Gwei Price * (1/1000000000)
```

So a 10 KB project at 100 gwei would be:

```
235 * 10000 * 100 * (1 / 1000000000)
235000000 / 1000000000
0.235 ETH
```

Artists have recently targeted between \~5-20 KB for their code (without the library), but obviously this will vary by project scope.

### Data Compression

We allow artists to compress data stored within their scripts (e.g. SVG data); but in the case where the logic of the script itself is compressed to the point of obfuscating the auditing process we may ask that artists remove this level of compression.

## Attribution

Much (generative art) source code is published under permissive copyleft licenses, making it available to be used by everybody and depending on the license even for commercial purposes. In case your project's code contains any code not written by yourself, please inform the Art Blocks team about it so the appropriate considerations and attributions can be made.

Common source code licenses (in creative coding):

- [CC BY](https://creativecommons.org/licenses/by/4.0/): The original author and license must be clearly and appropriately stated.
- [CC BY-SA](https://creativecommons.org/licenses/by-sa/4.0/): As CC BY, but all derivates must also be licensed under CC BY-SA.
- [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/): As CC BY-SA, but no commercial use is allowed.
- [MIT](https://choosealicense.com/licenses/mit/): similar to CC BY
- [GPL](https://choosealicense.com/licenses/gpl-3.0/): similar to CC BY-SA

There are many other free-to-use licenses commonly used on open source software. Please carefully read the full details on any licensed code you re-use or modify, before including it in your project.

## Testing on Goerli

Once your application is approved and your script is ready, you will test it out on an Art Blocks staging site running on one of Ethereum's test networks (Goerli). This will make sure there aren't any bugs or errors and that if it's working on Goerli, it will work on Mainnet. You can connect to this site by changing the network in your browser wallet (e.g. the very top button of MetaMask). You'll still be using the same wallet and address, except on the test network.

Note: If you don't have "Goerly ETH" ask a mod or previous artist, we'll send you some to play with. Or if you don't feel like waiting, request some from the faucet: - -
https://goerlifaucet.com/
https://goerli-faucet.pk910.de/ (POW faucet so this can run in the background and accumulate goerliETH over time)

### ROPSTEN > GOERLI UPGRADE

_As of Aug 2, 2022_

Ropsten is being deprecated entirely as a network. New testnet means new smart contracts: Ropsten artist-staging data will be preserved in a read-only state to be accessed at https://ropsten-artist-staging.artblocks.io/ after August 2nd.

The website for AB core will remain the same: You will still visit https://artist-staging.artblocks.io/, but you will be asked to connect with the Goerli Test Network rather than the Ropsten Test Network.

If you previously had a testnet shell on the Ropsten network, you may still access your project shell using https://ropsten-artist-staging.artblocks.io/ as a frozen read-only set of data. If you are a returning artist, please send([!badge Discord: madpinney#1183]) a DM to set up a Goerli project shell.

As a reminder, you can stock up on Goerli ETH here:
https://goerlifaucet.com/
https://goerli-faucet.pk910.de/ (POW faucet so this can run in the background and accumulate goerliETH over time)

### Interacting with your Project

If you made it this far, we have probably requested a project name and an Ethereum address from you. If not, that probably means your an artist who is in our pipeline and pending being onboarded–once we get you processed the following instructions will make more sense!

If you have provided a project name and Ethereum address to our team, this address you provided to our team will be used on mainnet and on Ropsten. So at this point change your network to Ropsten in MetaMask. On Ropsten, we'll practice uploading everything so that it all goes smooth on mainnet when the ETH is real. After loading the page and connecting your wallet, you should see a button labeled "Edit Project". A multi-tabbed form will pop up. You only need to focus on the following:

#### Project

This should all be self-explanatory. Just fill and submit each one separately.

#### Token

In this tab you'll set the price and max invocations for your project. If you're accepting ETH as payment you don't need to worry about "Updated Currency Information" and **should not change the currency address**. To reiterate, **do not** update the currency address to be your wallet address–this field should **only** be set if you are accepting payment for your project in some non-ETH ERC20-compliant token.

You can though specify any ERC20-compliant token if you choose, just give someone on the Art Blocks team a heads up that you wish to go down this route.

Set the baseURI: `https://api.artblocks.io/token/`

#### Script

Here you'll first specify the dependency of your project including the script type and the version number _of that dependency_. For most scripts, you can leave the version blank or enter 1. The aspect ratio is a single number. E.g. 1 or 0.75 etc. If your piece takes a certain amount of time to fully render you can type in the render delay to let the server know when to render the canvas.

Once you've submitted your script details add your script to the "Project Scripts" box. Remember, `tokenData.hash` is a global variable in the environment this script will live in, so you do not need to define `tokenData` in your script, just expect your script will have access to it.

If your script is big, consider minifying it. If your script is so big that you cannot fit it in a single transaction (you're getting an error when you submit), you may need to split it up and submit each part subsequently.

### Splitting

Once you have a working minified version of your project, a recommended way of splitting the file in parts for upload is to use the "split" command in Unix systems (Linux, Mac), like this:

```
split -b 10k filename.js new_filename
```

That will create an evenly distributed set of files with the splitted code, automatically. The maximum size you can upload to Artblocks per transaction is around 24KB (you can center that as -b 23900 in the split tool, since it does not take decimals)

if you are on Windows, you can use the same command if you have git bash, or a tool like [7-Zip](https://www.7-zip.org/), which allows you to split without compression.

#### Finishing Actions

Once all of the necessary fields have been submitted, you can then click "Purchases Paused" to test out the minting. Once your test mints are working in the livescript view, mint 20-40.

Make sure you've tested your code on multiple browsers (Chrome / Firefox / Safari) and on multiple device types (desktop / mobile) to ensure consistent output.

#### How does my project get those OpenSea attributes?

Once your project is selected to be included in one of the Art Blocks collections, the onboarding team will help you with this. The one thing to keep in mind is that all of the attributes you want displayed should be directly generated from the transaction hash and should not depend on any other randomness.

This script is essentially a copy of your rendering script but without any dependencies present (the server won't have access to them).

For full details on how to structure your project features, please see [Art Blocks Features Script](features.md#features-overview).
