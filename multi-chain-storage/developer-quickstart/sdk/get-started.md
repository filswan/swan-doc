---
description: This guide will explain how to install the mcs-client and its basic usage
---

# Get Started

## Prerequisites

* [Node.js](https://nodejs.org/en/) - This SDK was built using version v16.13.0 (npm v8.1.0)
* Polygon Mumbai Testnet Wallet - [Metamask Tutorial](../../mcp-user-guide/setup-metamask.md)
* Polygon Mumbai Testnet Alchemy RPC - [Alchemy Tutorial](../../mcp-user-guide/configure-metamask-with-alchemy-rpc-url.md#alchemypolygontometamaskinstructions-2.createalchemymumbaipolygonrpc)

Mumbai Testnet USDC and MATIC funds are also necessary - [Swan Faucet Tutorial](../../../development-resource/swan-token-contract/acquire-testnet-usdc-and-matic-tokens.md)

## Installation

Install the package using npm. It is recommended to create a new directory for a new project.

```
npm install mcs-client
```

## Environment Variables

Once you have your Mumbai wallet and RPC URL, create a file named `.env` and store your wallet's private key and the RPC URL.

```
PRIVATE_KEY=<PRIVATE_KEY>
RPC_URL=https://polygon-mumbai.g.alchemy.com/v2/<API_KEY>
```

{% hint style="info" %}
Be careful not to expose this information! \
Revealing your private key to others will give them access to your wallet
{% endhint %}

## Upload File Example

Here is a simple example to upload a single file to MCS. Made a new file named `upload.js`

```
require('dotenv').config()
const { mcsClient } = require('mcs-client')

// set up mcs-client
const client = new mcsClient({
  privateKey: process.env.PRIVATE_KEY,
  rpcUrl: process.env.RPC_URL,
})

async function main() {
  const testFile = JSON.stringify({ address: client.publicKey })
  const fileArray = [{ fileName: 'testFile.json', file: testFile }]

  const uploadResponse = await client.upload(fileArray)
  console.log(uploadResponse)
}

main()
```

Use the command `node upload.js` to run the code. This snippet creates the MCS-Client instance, creates a JSON file with your wallet address, and uploads the file to MCS.

## Documentation Note

The following documentation for this client will assume you have a MCS client instantiated. Using the `client` variable for the following examples.

```
const client = new mcsClient({
  privateKey: process.env.PRIVATE_KEY,
  rpcUrl: process.env.RPC_URL,
})
```

and all following snippets will replace the contents of the `main()` function above.
