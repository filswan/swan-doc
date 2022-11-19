---
description: Get payment information of a previous upload
---

# Get Payment Info

```python
McsAPI.get_payment_info(payload_cid, source_file_upload_id)
```

odeThis API retrieve the payment information use the source file upload id of an upload. This id can be retrieved use the view all uploads API.

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

```json
{
    "status": "success",
    "data": {
        "w_cid": <>,
        "pay_amount": <>,
        "pay_tx_hash": <>,
        "token_address":  <>
    }
```
