---
description: Upload file(s) to MCS using the MCS SDK
---

# Upload Files

You can use the upload function to upload a single file to the FilSwan IPFS gateway. The function takes your MetaMask wallet address and the absolute path(or relative) of the file for upload.

<pre class="language-python"><code class="lang-python"><strong>OnchainAPI.upload_file(self, wallet_address, file_path)
</strong></code></pre>

Let's use the same instance of OnchainAPI we created for authorization.

{% code lineNumbers="true" %}
```python
file_path = "/<file_name>"
upload_file = onchain_api.stream_upload_file(wallet_address, file_path)
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
