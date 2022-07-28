---
description: Upload large files using stream upload.
---

# Stream Upload Files

`McsAPI.stream_upload_file(wallet_address, file_path)`

Stream upload can be used in the same way as normal upload.

```
def test_stream_upload_file_pay():
    wallet_address = wallet_info['wallet_address']

    api = McsAPI()
    # upload file to mcs
    file_path = "/*"
    upload_file = api.stream_upload_file(wallet_address, file_path)
```

### Parameters

* wallet\_address: MetaMask wallet address.
* file\_path: Absolute path of the file for upload.
