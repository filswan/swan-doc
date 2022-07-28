---
description: Get Details about a specific file
---

# Get File Details

`McsAPI.get_payment_info(self, payload_cid, wallet_address, source_file_upload_id)`

The following code example gets the file details of an uploaded file. This method takes the upload id of the file, and the deal id of the file.

```
    def get_payment_info(self, payload_cid, wallet_address, source_file_upload_id):
        params = {}
        if payload_cid:
            params['payload_cid'] = payload_cid
        if wallet_address:
            params['wallet_address'] = wallet_address
        if wallet_address:
            params['source_file_upload_id'] = source_file_upload_id
        return self._request_with_params(GET, PAYMENT_INFO, params, None)
```

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
      ipfs_url: <'https://calibration-ipfs.filswan.com/ipfs/Qm...'>,
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
