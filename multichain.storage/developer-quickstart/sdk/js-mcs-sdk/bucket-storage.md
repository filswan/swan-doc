---
description: Guide to multichain.storage's Bucket Storage
---

# Bucket Storage

In a multichain storage system, a bucket is a logical container that stores folders or files. Each bucket has a unique name and can contain any number of folders and files. Folders are virtual containers that organize files and help manage data, and files are individual data objects that can be of any type or format.

### Create a Bucket

`createBucket(bucketName)`

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_NAME = ''

  const mcs = await mcsSDK.initialize({
    apiKey: process.env.API_KEY,
    accessToken: process.env.ACCESS_TOKEN,
  })
  
  let createBucketResponse = await mcs.createBucket(BUCKET_NAME)
}

main()
```

#### Parameters

* **bucketName**: The name of the bucket&#x20;

#### Return

<pre class="language-javascript"><code class="lang-javascript"><strong>{ status: 'success', data: &#x3C;bucket_uid> }
</strong></code></pre>

### Get Bucket(s)

`getBuckets()`, `getBucketList()`

These two functions are actually interchangeable, it will return the list of buckets.

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  const mcs = await mcsSDK.initialize({
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
  
  let bucketInfo = await mcs.getBuckets()
  console.log(bucketInfo)
}

main()
```

#### Return

```javascript
{
  status: 'success',
  data: [
    {
      bucket_uid: '233...1cd',
      address: '0x1f...4C6',
      max_size: 34359738368,
      size: 0,
      is_free: true,
      payment_tx: '',
      is_active: true,
      is_deleted: false,
      bucket_name: 'test-bucket',
      file_number: -1,
      id: 411,
      created_at: '2023-02-23T20:35:28Z',
      updated_at: '2023-02-23T20:35:28Z',
      deleted_at: null
    }
  ]
}
```

### Delete Bucket

`deleteBucket(bucketName)`

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_NAME = ''

  const mcs = await mcsSDK.initialize({
    apiKey: process.env.API_KEY,
    accessToken: process.env.ACCESS_TOKEN,
  })
  
  let deleteBucketResponse = await mcs.deleteBucket(BUCKET_NAME)
}

main()
```

#### Parameters

* **bucketName**: The name of the bucket

#### Return

```javascript
{ status: 'success' }
```

### Rename Bucket

`renameBucket(oldName, newName)`

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_NAME = ''
  const NEW_BUCKET_NAME = ''

  const mcs = await mcsSDK.initialize({
    apiKey: process.env.API_KEY,
    accessToken: process.env.ACCESS_TOKEN,
  })
  
  let renameResponse = await mcs.renameBucket(BUCKET_NAME, NEW_BUCKET_NAME)
}

main()
```

#### Parameters

* **oldName**: The name of the bucket&#x20;
* **newName:** The new name of the bucket

#### Return

```javascript
{ status: 'success', data: 'rename success' }
```

### Create Folder

`createFolder(bucketName, objectName)`

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_NAME = ''
  const OBJECT_NAME = ''

  const mcs = await mcsSDK.initialize({
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
  
  let folderResponse = await mcs.createFolder(BUCKET_NAME, OBJECT_NAME)
  console.log(folderResponse)
}

main()
```

#### Parameters

* **bucketName**: The name of the bucket
* **objectName:** The name of the folder path inside the bucket

#### Return

```javascript
{ status: 'success', data: '<folder_name>' }
```

### Upload File

`uploadToBucket(bucketName, objectName, filePath, replace=false)`

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_NAME = ''
  const OBJECT_NAME = ''
  const FILE_PATH = ''

  const mcs = await mcsSDK.initialize({
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
  
  let uploadResponse = await mcs.uploadToBucket(BUCKET_NAME, OBJECT_NAME, FILE_PATH)
  console.log(uploadResponse)
}

main()
```

#### Parameters

* **bucketName**: The name of the bucket
* **objectName**: The name of the file path inside the bucket (ex: folder1/folder2/file.png)
* **filePath**: The local path to the file (ex: Desktop/images/file.png)
* **replace:** Bucket Storage does not allow files of the same name, set replace to true to replace the existing file

#### Return

```javascript
{
  status: 'success',
  data: {
    file_id: <file_id>,
    file_hash: '7e...96',
    file_is_exist: false,
    ipfs_is_exist: false,
    size: 63447054,
    payload_cid: 'Qme...kMr',
    ipfs_url: 'https://ipfs.multichain.storage/ipfs/Qm...'
  }
}
```

### Download File

`downloadFile(bucketName, objectName, outputPath='.')`

Downloads an uploaded file in a bucket, to the desired `outputDirectory`

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_NAME = ''
  const OBJECT_NAME = ''
  const OUTPUT_PATH = '.'

  const mcs = await mcsSDK.initialize({
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY
  })

  let downloadResponse = await mcs.downloadFile(BUCKET_NAME, OBJECT_NAME, OUTPUT_PATH)
}

main()
```

#### Parameters

* **bucketName**: The name of the bucket
* **objectName**: Path of the object you want to download (ex: folder1/folder2/file.png)
* **outputPath**: Output path of the downloaded file (default is '.' i.e current directory)

#### Return

```javascript
{ status: 'success' }
```

### Delete File

`deleteFile(bucketName, objectName)`

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_NAME = ''
  const OBJECT_NAME = ''

  const mcs = await mcsSDK.initialize({
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
  
  let deleteResponse = await mcs.deleteFile(BUCKET_NAME, OBJECT_NAME)
  console.log(deleteResponse)
}

main()
```

#### Parameters

* **bucketName**: The name of the bucket
* **objectName:** The name of the object to delete

#### Return

```javascript
{ status: 'success' }
```

### Get File List

`getFileList(bucketName, params), getFiles(bucketName, params)`

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_NAME = ''
  const PARAMS = {
    prefix: '',
    limit: 10,
    offset: 0
  } 

  const mcs = await mcsSDK.initialize({
    apiKey: process.env.API_KEY,
    accessToken: process.env.ACCESS_TOKEN,
  })
  
  let fileList = await mcs.getFileList(BUCKET_NAME, PARAMS)
  console.log(fileList)
}

main()
```

#### Parameters

* **bucketName**: The name of the bucket
* **params**
  * **prefix:** the folder prefix if you want the list of files in a subfolder
  * **limit:** number of returned files
  * **offset:** page number&#x20;

#### Return

```javascript
{
  file_list: [
    {
      name: 'f1',
      address: '0x1...4C6',
      prefix: '',
      bucket_uid: '233...1cd',
      file_hash: '',
      size: 0,
      payload_cid: '',
      ipfs_url: '',
      pin_status: '',
      is_deleted: false,
      is_folder: true,
      object_name: 'f1',
      id: 6548,
      created_at: '2023-02-24T17:33:56Z',
      updated_at: '2023-02-24T17:33:56Z',
      deleted_at: null
    }
    ...
  ],
  count: 1
}
```

### Get File Info

`getFileInfo(bucketName, objectName)`

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_NAME = ''
  const OBJECT_NAME = ''

  const mcs = await mcsSDK.initialize({
    apiKey: process.env.API_KEY,
    accessToken: process.env.ACCESS_TOKEN,
  })
  
  let fileInfo = await mcs.getFileInfo(BUCKET_NAME, OBJECT_NAME)
  console.log(fileInfo)
}

main()
```

#### Parameters

* **bucketName**: The name of the bucket
* **objectName:** The name of the object

#### Return

```javascript
{
  status: 'success',
  data: {
    name: '<file_name>',
    address: '0x1ff...4C6',
    prefix: '',
    bucket_uid: '233...1cd',
    file_hash: '',
    size: 0,
    payload_cid: '',
    ipfs_url: '',
    pin_status: '',
    is_deleted: false,
    is_folder: true,
    object_name: '<object_name>',
    id: 6548,
    created_at: '2023-02-24T17:33:56Z',
    updated_at: '2023-02-24T17:33:56Z',
    deleted_at: null
  }
}
```
