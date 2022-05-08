---
description: Upload file(s) to MCS using the MCS Client
---

# Upload Files

`upload(fileArray, options)`

You can use the upload function to upload an array of file(s) to FilSwan IPFS gateway. The array holds a list of objects, and returns an array of response objects. Using `fs` is a simple way to read the file data. The options object is also optional to customize the upload.

```
const fileArray = [
  { fileName: 'file1', file: fs.createReadStream('./file1.txt') },
  { fileName: 'file2', file: fs.createReadStream('./file2.txt') },
]

//optional, showing default options
const options = {
  delay: 1000, // delay between upload API calls for each file. May need to be raised for larger files
  duration: 180, // the number of days to store the file on the Filecoin network.
  fileType: 0, // set to 1 for nft metadata files. type 1 files will not show on the UI.
}

const uploadResponses = await client.upload(fileArray, options)
console.log(uploadResponses)
```

### Parameters

* **fileArray**: array of objects
  * **fileName**: name of file
  * **file**: file contents (using `fs` is a simple way to get the file contents)
* **options**: an optional object can also be passed to specify certain parameters:
  * **delay**: delay in milliseconds between upload API calls. Default is 1000, but may need to be increased for many larger files
  * **duration**: Number of days to store your file on the Filecoin network. (default 180)
  * **fileType**: Files of type one will be hidden from the upload list and the UI. NFT metadata files are type 1. (default 0)

### Return

This function returns an array of the upload API responses.