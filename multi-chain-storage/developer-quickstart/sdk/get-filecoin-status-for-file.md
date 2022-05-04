# Get Filecoin Status for File

`checkStatus(dealCid)`

The following code example returns the FIlecoin storage status of a paid file. This method requires the deal cid of the deal. This can also be obtained by the listUploads method.

```
const PAYLOAD_CID = ''
 
// search for file info to get deal_cid
const uploadInfo = await client.listUploads(client.publicKey, PAYLOAD_CID)
const dealCid = uploadInfo.data[0].deal_cid
 
// not every file will have a deal cid available
if (dealCid) {
  const fileStatus = await client.checkStatus(dealCid)
  console.log(fileStatus)
} else {
  console.log('deal_cid not found')
}
```

### Parameters

* **dealCid**: deal cid of the file, not all files will have

### Return

Returns the response from the `/deal/log/` API
