---
description: This guide will explain how to install the js-mcs-sdk and its basic usage
---

# Get Started

## Prerequisites

* [Node.js](https://nodejs.org/en/) - This SDK was built using version v16.13.0 (npm v8.1.0)
* Metamask wallet - [Metamask Tutorial](../../../mcp-user-guide/setup-metamask.md)
* API Key and Access Token - Obtained via [https://multichain.storage](https://multichain.storage/)

## Installation

Install the package using npm. It is recommended to create a new directory for a new project. Run the init command to setup a package.json file

```
npm init -y
npm install js-mcs-sdk
```

## Environment Variables

Set your API Key and Access Token as environment variables in a `.env` file. Optionally include your wallet's private key and RPC-URL.

```
API_KEY=<API_KEY>
ACCESS_TOKEN=<ACCESS_TOKEN>

# optional
PRIVATE_KEY=<PRIVATE_KEY>
RPC_URL=<RPC_URL>
```

{% hint style="info" %}
Be careful not to expose this information! \
Revealing your private key to others will give them access to your wallet.
{% endhint %}

## Writing SDK Scripts

To begin writing a script utilizing the SDK, create a new `.js` file.&#x20;

At the top of this file, require the necessary packages. Since these functions are [asynchronous](https://javascript.info/async-await), we will need to create an `async` function to run the SDK methods.

Now inside the asynchronous `main` function, we can initialize the SDK

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // initialize js-mcs-sdk
  const mcs = await mcsSDK.initialize({
    apiKey: process.env.API_KEY,
    accessToken: process.env.ACCESS_TOKEN,
  })
  
  // code snippets found in the documentation go here
  // ...
}

main()
```

Optionally, you can pass `privateKey` to use the onChain Storage upload and payment functions and pass `rpcUrl` if you wish to use your own RPC URL (this SDK uses [https://polygon-rpc.com/](https://polygon-rpc.com/) by default).

{% hint style="info" %}
This is the boilerplate code for all snippets found in the SDK documentation
{% endhint %}

## Upload File Example

Here is a simple example to upload a single file to MCS. Made a new file named `upload.js`

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // initialize js-mcs-sdk
  const mcs = await mcsSDK.initialize({
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
    privateKey: process.env.PRIVATE_KEY,
  })

  const testFile = JSON.stringify({ address: mcs.walletAddress })
  const fileArray = [{ fileName: `${mcs.walletAddress}.txt`, file: testFile }]

  const uploadResponse = await mcs.upload(fileArray)
  console.log(uploadResponse)
}

main()
```

Use the command `node upload.js` to run the code. This snippet creates the MCS SDK instance, creates a JSON file with your wallet address, and uploads the file to MCS.
