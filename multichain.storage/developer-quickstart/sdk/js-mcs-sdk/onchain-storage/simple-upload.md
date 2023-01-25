---
description: Demo for using MCS simple upload
---

# Simple Upload

## Writing SDK Scripts

To begin writing a script utilizing the SDK, create a new `.js` file. Let's create a file named `test.js` for this guide.

At the top of this file, `require` the `mcsSDK` class from the `js-mcs-sdk` package for the script.

{% code lineNumbers="true" %}
```javascript
const { mcsSDK } = require("js-mcs-sdk");
```
{% endcode %}

Now we can begin writing the demo script.

### Initialize SDK

To initialize the SDK, require the environment variables in your `.env` file using `dotenv`

{% code lineNumbers="true" %}
```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // initialize js-mcs-sdk
  const mcs = await mcsSDK.initialize({
    apiKey: process.env.API_KEY,
    accessToken: process.env.ACCESS_TOKEN,
    chainName: 'polygon.mainnet',
  })
}

main()
```
{% endcode %}

### Simple Upload File

To use the fastest way to upload a file to [multichain.storage](https://multichain.storage), we need to call the `upload()` function.

```javascript
let uploadResponse = await mcs.upload([
  {
    fileName: '<FILE_NAME>',
    file: fs.createReadStream('<FILE_PATH>'),
  },
])
console.log(uploadResponse)
```

The upload function uploads the file to the IPFS server. MCS currently has 10GB of free upload per month for each wallet. The `need_pay` will indicates if a file is under the coverage of free upload. When `need_pay == 1` then the file needs to be paid and it is free when `need_pay == 0`

### Full Demo Code

{% code lineNumbers="true" %}
```javascript
require('dotenv').config()
const fs = require('fs')
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  const FILE_NAME = '<FILE_NAME>'
  const FILE_PATH = '<FILE_PATH>'

  const mcs = await mcsSDK.initialize({
    apiKey: process.env.API_KEY,
    accessToken: process.env.ACCESS_TOKEN,
  })

  const fileArray = [
    { fileName: FILE_NAME, file: fs.createReadStream(FILE_PATH) },
  ]

  const uploadResponse = await mcs.upload(fileArray)
  console.log(uploadResponse)
}

main()
```
{% endcode %}
