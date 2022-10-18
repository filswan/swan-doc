---
description: This guide will explain how to install the js-mcs-sdk and its basic usage
---

# Get Started

## Prerequisites

* [Node.js](https://nodejs.org/en/) - This SDK was built using version v16.13.0 (npm v8.1.0)
* Metamask wallet - [Metamask Tutorial](../../../mcp-user-guide/setup-metamask.md)

USDC and MATIC funds are also necessary

## Installation

Install the package using npm. It is recommended to create a new directory for a new project. Run the init command to setup a package.json file

This version of MCS interacts with the Polygon mainnet. The corresponding UI is [here](https://www.multichain.storage/)

```
npm init -y
npm install js-mcs-sdk
```

## Environment Variables

Once you have your Metamask wallet and RPC URL(s), create a file named `.env` in your project directory and store your wallet's private key and the RPC URL.&#x20;

```
PRIVATE_KEY=<PRIVATE_KEY>
RPC_URL=https://polygon-rpc.com/
```

{% hint style="info" %}
Be careful not to expose this information! \
Revealing your private key to others will give them access to your wallet.
{% endhint %}

## Writing SDK Scripts

To begin writing a script utilizing the SDK, create a new `.js` file.&#x20;

At the top of this file, require the necessary packages. Since these functions are [asynchronous](https://javascript.info/async-await), we will need to create an `async` function to run the SDK methods.

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // code snippets found in the documentation go here
}

main()
```

Now inside the asynchronous `main` function, we can initialize the SDK

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk-staging')

async function main() {
  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    rpcUrl: process.env.RPC_URL,
  })
  
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
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    rpcUrl: process.env.RPC_URL,
  })

  const testFile = JSON.stringify({ address: mcs.publicKey })
  const fileArray = [{ fileName: `${mcs.publicKey}.txt`, file: testFile }]

  const uploadResponse = await mcs.upload(fileArray)
  console.log(uploadResponse)
}

main()
```

Use the command `node upload.js` to run the code. This snippet creates the MCS SDK instance, creates a JSON file with your wallet address, and uploads the file to MCS.
