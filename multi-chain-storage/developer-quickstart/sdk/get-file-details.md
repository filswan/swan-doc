# Get File Details

`getFileDetails(payloadCid, dealId)`

The following code example gets the file details of an uploaded file. This method takes the payload cid of the file, and the deal id of the file. The deal id can be obtained by the listUploads method

```
const PAYLOAD_CID = ''
const DEAL_ID = ''
 
console.log(await client.getFileDetails(PAYLOAD_CID, DEAL_ID))
```

### Parameters

* **payloadCid**: payload cid of the file
* **dealId**: deal id of the file

### Return

Returns the response from the `/deal/detail/` API
