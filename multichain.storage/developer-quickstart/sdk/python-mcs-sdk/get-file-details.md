---
description: Get Details about a specific file
---

# Get File Details

`McsAPI.get_payment_info(self, payload_cid, wallet_address, source_file_upload_id)`

The following code example gets the file details of an uploaded file. This method takes the upload id of the file, and the deal id of the file.

{% code lineNumbers="true" %}
```python
file_data = upload_file["data"]
payload_cid, source_file_upload_id, nft_uri, file_size, w_cid = file_data['payload_cid'], file_data[
    'source_file_upload_id'], file_data['ipfs_url'], file_data['file_size'], file_data['w_cid']
# get deal details
return deal_detail = api.get_deal_detail(wallet_address, source_file_upload_id)
```
{% endcode %}

### Parameters

* **source\_file\_upload\_id**: upload id of the file
* **payload\_cid**: not required

### Return

Returns the response from the `/deal/detail/` API

```
{
  status: 'success',
  data: {
    dao_signature: [ [Object], [Object], [Object], [Object] ],
    dao_threshold: 2,
    source_file_upload_deal: {
      deal_id: <ID>,
      deal_cid: '',
      message_cid: <'bafy...'>,
      height: <NUMBER>,
      piece_cid: <'...'>,
      verified_deal: <BOOLEAN>,
      storage_price_per_epoch: 0,
      signature: '',
      signature_type: '',
      created_at: <TIME>,
      piece_size_format: null,
      start_height: <NUMBER>,
      end_height: <NUMBER>,
      client: <'f...'>,
      client_collateral_format: '000000000000000000',
      provider: <'f...'>,
      provider_tag: '',
      verified_provider: 0,
      provider_collateral_format: '000000000000000000',
      status: 0,
      network_name: 'filecoin_mainnet',
      storage_price: 0,
      ipfs_url: <'https://ipfs.multichain.storage/ipfs/Qm...'>,
      file_name: <FILE_NAME>,
      w_cid: <UNIQUE_CID>,
      car_file_payload_cid: <'bafy...'>,
      locked_at: <TIME>,
      locked_fee: <AMOUNT>,
      unlocked: <BOOLEAN>
    }
  }
}
```
