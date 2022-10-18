---
description: Upload file(s) to MCS using the MCS SDK
---

# Upload Files

You can use the upload function to upload a single file to FilSwan IPFS gateway. The function takes your MetaMask wallet address and the absolute path(or relative) of the file for upload.

```python
McsAPI.upload_file(self, wallet_address, file_path)
```

Let's use the same instance of McsAPI we created for authorization.

{% code lineNumbers="true" %}
```python
file_path = "/<file_name>"
upload_file = api.upload_file(wallet_address, file_path)
```
{% endcode %}

The normal upload function will work fine for smaller files. However, stream upload is the recommended method to upload files. To use stream upload:

```python
McsAPI.stream_upload_file(self, wallet_address, file_path)
```

An example using stream upload

{% code lineNumbers="true" %}
```python
file_path = "/<file_name>"
upload_file = api.stream_upload_file(wallet_address, file_path)
```
{% endcode %}

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
    ipfs_url: <'https://ipfs.multichain.storage/ipfs/Qm...'>,
    file_size: <FILE_SIZE>,
    w_cid: <UNIQUE_CID>,
    status: <Free/Pay>
  }
}
```
