# List Files

`listUploads(walletAddress, payloadCid, fileName, pageNumber, pageSize)`

The following code example lists a user's uploaded files. The list can also be searched by payload cid or by file name.

```
console.log(await client.listUploads())
 
// search by payload cid
console.log(await client.listUploads(client.publicKey, payloadCid)) 

// search by file name
console.log(await client.listUploads(client.publicKey, '', 'fileName')
```

### Parameters

* **walletAddress**: lists the files uploaded by this account (required)
* **payloadCid**: filter by this payload cid
* **fileName**: filter by this file name
* **pageNumber**: page number (default 1)
* **pageSize**: number of results in a page (default 10)

### Return

Returns an array containing some details of the file(s).
