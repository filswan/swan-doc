# List Files

`getUploads(walletAddress, payloadCid, fileName, orderBy, isAscend, status, isMinted, pageNumber, pageSize)`

The following code example lists a user's uploaded files. The list can be searched by file name, and also be filtered or sorted.

```
const FILE_NAME = ''
const ORDER_BY = ''
const IS_ASCEND = ''
const STATUS = ''
const IS_MINTED = ''
const PAGE_NUMBER = 1
const PAGE_SIZE = 10

const uploads = await mcs.getUploads(
  mcs.publicKey,
  FILE_NAME,
  ORDER_BY,
  IS_ASCEND,
  STATUS,
  IS_MINTED,
  PAGE_NUMBER,
  PAGE_SIZE,
)

console.log(uploads.data.source_file_upload)
```

### Parameters

* **walletAddress**: lists the files uploaded by this account (required)
* **fileName**: filter by this file name
* **orderBy**: sort the list by file name, file size, or upload time (default)
* **isAscend**: y for ascending list, otherwise descend (default)
* **status**: Pending, Processing, Refundable, Refunded, Success or other
* **isMinted**: y, n, all (default)
* **pageNumber**: page number (default 1)
* **pageSize**: number of results in a page (default 10)

Only the walletAddress parameter is required, the rest are optional.

### Return

Returns an array containing some details of the file(s).
