---
description: Upload file(s) to MCS using the MCS SDK
---

# Upload Files

`upload_file(wallet_address, file_path)`

You can use the upload function to upload a single file to FilSwan IPFS gateway.

```
def test_upload_file(wallet_info):
    wallet_address = wallet_info['wallet_address']

    api = McsAPI()
    # upload file to mcs
    filepath = "/*"
    father_path = os.path.abspath(os.path.dirname(__file__))
    upload_file = api.upload_file(wallet_address, father_path + filepath)
```

### Parameters

* wallet\_address: MetaMask wallet address.
* file\_path: Location of the file for upload.

### Return

This function returns the upload API responses.

```
{
  status: 'success',
  data: {
    source_file_upload_id: <ID>,
    payload_cid: <'Qm...'>,
    ipfs_url: <'https://calibration-ipfs.filswan.com/ipfs/Qm...'>,
    file_size: <FILE_SIZE>,
    w_cid: <UNIQUE_CID>
  }
}
```
