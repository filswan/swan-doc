---
description: Upload file(s) to MCS using the MCS SDK
---

# Upload Files

`McsAPI.upload_file(wallet_address, file_path)`

You can use the upload function to upload a single file to FilSwan IPFS gateway. The function takes your MetaMask wallet address and the absolute path of the file for upload.

```
def test_upload_file(wallet_info):
    wallet_address = wallet_info['wallet_address']

    api = McsAPI()
    # upload file to mcs
    file_path = "/*"
    upload_file = api.upload_file(wallet_address, file_path)
```

### Parameters

* wallet\_address: MetaMask wallet address.
* file\_path: Absolute path of the file for upload.

### Return

This function returns the upload API responses. This includes `source_file_upload_id`, `file_size` _and_ `w_cid` that will be used for payments.

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
