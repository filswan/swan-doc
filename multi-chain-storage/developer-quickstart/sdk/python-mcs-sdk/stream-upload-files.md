---
description: Upload large files using stream upload.
---

# Stream Upload Files

`stream_upload_file(self, wallet_address, file_path)`

Stream upload can be used in the same way as normal upload.

```
def test_stream_upload_file_pay():
    wallet_address = wallet_info['wallet_address']

    api = McsAPI()
    # upload file to mcs
    filepath = "/images/log_mcs.png"
    father_path = os.path.abspath(os.path.dirname(__file__))
    upload_file = api.stream_upload_file(wallet_address, father_path + filepath)
```

### Parameters

* wallet\_address: MetaMask wallet address.
* file\_path: Location of the file for upload.
