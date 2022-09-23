---
description: This guide will explain how to install the js-mcs-sdk and its basic usage
---

# Get Started

## Prerequisites

* [Node.js](https://nodejs.org/en/) - This SDK was built using version v16.13.0 (npm v8.1.0)
* Metamask wallet - [Metamask Tutorial](../../../mcp-user-guide/setup-metamask.md)
* Web3 RPC URL (for supported chains) - [Alchemy Tutorial](../../../mcp-user-guide/configure-metamask-with-alchemy-rpc-url.md#alchemypolygontometamaskinstructions-2.createalchemymumbaipolygonrpc)

Testnet USDC and MATIC funds are also necessary for test versions - [Swan Faucet Tutorial](../../../../development-resource/swan-token-contract/acquire-testnet-usdc-and-matic-tokens.md)

## Installation

Install the package using npm. It is recommended to create a new directory for a new project. Run the init command to setup a package.json file

#### Polygon Mainnet Version

This version of MCS interacts with the Polygon mainnet. The corresponding UI is [here](https://www.multichain.storage/)

```
npm init -y
npm install js-mcs-sdk
```

#### Calibration Environment

The calibration environment is meant for testing, allowing users to use the Mumbai testnet and Binance testnet. [Visit the UI](https://calibration-mcs.filswan.com/)

```
npm init -y
npm install js-mcs-sdk-calibration
```

#### Staging Environment

This version is for the [staging environment of MCS](https://mcs.filswan.com/).&#x20;

```
npm init -y
npm install js-mcs-sdk-staging
```

## Environment Variables

Once you have your Metamask wallet and RPC URL(s), create a file named `.env` in your project directory and store your wallet's private key and the RPC URL(s). Depending on which version you choose, you do not need all the different RPC\_URLs.

<pre><code>PRIVATE_KEY=&#x3C;PRIVATE_KEY>
MUMBAI_RPC_URL=https://polygon-mumbai.g.alchemy.com/v2/&#x3C;API_KEY>
TBNC_RPC_URL=https://data-seed-prebsc-1-s1.binance.org:8545
<strong>POLYGON_RPC_URL=https://polygon-rpc.com/</strong></code></pre>

{% hint style="info" %}
Be careful not to expose this information! \
Revealing your private key to others will give them access to your wallet.
{% endhint %}

## Writing SDK Scripts

To begin writing a script utilizing the SDK, create a new `.js` file. Let's create a file named `demo.js`

At the top of this file, require the necessary packages for the script and initialize the SDK. It depends on which environment you wish to interact with

```
require('dotenv').config()
// depending on which version you installed or want to use
const { mcsSDK } = require('js-mcs-sdk')
// const { mcsSDK } = require('js-mcs-sdk-calibration')
// const { mcsSDK } = require('js-mcs-sdk-staging')

const mcs = new mcsSDK({
  privateKey: process.env.PRIVATE_KEY,
  rpcUrl: process.env.<NETWORK>_RPC_URL, // replace with correct RPC_URL name from .env
  network: 'mumbai' // or 'tbnc' but this parameter is only for calibration environment
})
```

{% hint style="info" %}
The `network` parameter is only used in the calibration environment. It must correspond to the correct RPC\_URL network
{% endhint %}

Now we can begin using the SDK methods. Since these functions are [asynchronous](https://javascript.info/async-await), we will need to create an `async` function to run the SDK methods. Here is an example for the staging version:

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk-staging')

const mcs = new mcsSDK({
  privateKey: process.env.PRIVATE_KEY,
  rpcUrl: process.env.MUMBAI_RPC_URL,
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
const { mcsSDK } = require('js-mcs-sdk')

// set up js-mcs-sdk
const mcs = new mcsSDK({
  privateKey: process.env.PRIVATE_KEY,
  rpcUrl: process.env.POLYGON_RPC_URL,
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
