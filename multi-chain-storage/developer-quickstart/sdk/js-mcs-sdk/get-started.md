---
description: This guide will explain how to install the js-mcs-sdk and its basic usage
---

# Get Started

## Prerequisites

* [Node.js](https://nodejs.org/en/) - This SDK was built using version v16.13.0 (npm v8.1.0)
* Polygon Mumbai Testnet Wallet - [Metamask Tutorial](../../../mcp-user-guide/setup-metamask.md)
* Polygon Mumbai Testnet Alchemy RPC - [Alchemy Tutorial](../../../mcp-user-guide/configure-metamask-with-alchemy-rpc-url.md#alchemypolygontometamaskinstructions-2.createalchemymumbaipolygonrpc)

Mumbai Testnet USDC and MATIC funds are also necessary - [Swan Faucet Tutorial](../../../../development-resource/swan-token-contract/acquire-testnet-usdc-and-matic-tokens.md)

## Installation

Install the package using npm. It is recommended to create a new directory for a new project. Run the init command to setup a package.json file

```
npm init -y
npm install js-mcs-sdk
```

## Environment Variables

Once you have your Mumbai wallet and RPC URL, create a file named `.env` in your project directory and store your wallet's private key and the RPC URL.

```
PRIVATE_KEY=<PRIVATE_KEY>
RPC_URL=https://polygon-mumbai.g.alchemy.com/v2/<API_KEY>
```

{% hint style="info" %}
Be careful not to expose this information! \
Revealing your private key to others will give them access to your wallet.
{% endhint %}

## Writing SDK Scripts

To begin writing a script utilizing the SDK, create a new `.js` file. Let's create a file named `demo.js`

At the top of this file, require the necessary packages for the script.

```
// demo.js
require('dotenv').config()
const { mcsSdk } = require('js-mcs-sdk')
```

* `require('donenv').config()` will add the variables in your `.env` file to `process.env`
* `const { mcsSdk } = require('js-mcs-sdk')` will require the SDK

Next, after requiring the SDK, we still need to initialize it

```
require('dotenv').config()
const { mcsSdk } = require('js-mcs-sdk')

// set up js-mcs-sdk
const mcs = new mcsSdk({
  privateKey: process.env.PRIVATE_KEY,
  rpcUrl: process.env.RPC_URL,
})
```

Now we can begin using the SDK methods. Since these functions are [asynchronous](https://javascript.info/async-await), we will need to create an `async` function to run the SDK methods.

```
require('dotenv').config()
const { mcsSdk } = require('js-mcs-sdk')

// set up js-mcs-sdk
const mcs = new mcsSdk({
  privateKey: process.env.PRIVATE_KEY,
  rpcUrl: process.env.RPC_URL,
})

async function main() {
  // code snippets found in the documentation go here
}

main()
```

{% hint style="info" %}
This is the boilerplate code for all snippets found in the SDK documentation
{% endhint %}

## Upload File Example

Here is a simple example to upload a single file to MCS. Made a new file named `upload.js`

```
require('dotenv').config()
const { mcsSdk } = require('js-mcs-sdk')

// set up js-mcs-sdk
const mcs = new mcsSdk({
  privateKey: process.env.PRIVATE_KEY,
  rpcUrl: process.env.RPC_URL,
})

async function main() {
  const testFile = JSON.stringify({ address: mcs.publicKey })
  const fileArray = [{ fileName: `${mcs.publicKey}.txt`, file: testFile }]

  const uploadResponse = await mcs.upload(fileArray)
  console.log(uploadResponse)
}

main()
```

Use the command `node upload.js` to run the code. This snippet creates the MCS SDK instance, creates a JSON file with your wallet address, and uploads the file to MCS.
