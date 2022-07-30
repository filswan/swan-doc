---
description: View your uploaded files
---

# List Files

`McsAPI.get_user_tasks_deals(self, wallet_address)`

The following code example lists a user's uploaded files. The list can be searched by file name, and also be filtered or sorted.

```
def list_files(wallet_info):
    wallet_address = wallet_info['wallet_address']

    api = McsAPI()
    return api.get_user_tasks_deals(wallet_address)
```

### Parameters

* **wallet\_address**: lists the files uploaded by this account (required)

### Other Parameters of the API&#x20;

Can be used by editing the original get\_user\_tasks\_deals function.

* **file\_name**: filter by this file name
* **order\_by**: sort the list by file name, file size, or upload time (default)
* **is\_ascend**: y for ascending list, otherwise descend (default)
* **status**: Pending, Processing, Refundable, Refunded, Success or other
* **is\_minted**: y, n, all (default)
* **page\_number**: page number (default 1)
* **page\_size**: number of results in a page (default 10)

Only the wallet\_address parameter is required, the rest are optional.

### Return

Returns an array containing some details of the file(s).

```
[
  {
    source_file_upload_id: <ID>,
    car_file_id: <ID>,
    file_name: <FILE_NAME>,
    file_size: <FILE_SIZE>,
    upload_at: <TIME>,
    duration: 525,
    ipfs_url: <'https://calibration-ipfs.filswan.com/ipfs/Qm...'>,
    pin_status: 'Pinned',
    payload_cid: <'bafy...'>,
    w_cid: <UNIQUE_CID>,
    status: 'Processing',
    deal_success: <BOOLEAN>,
    is_minted: <BOOLEAN>,
    token_id: <ID>,
    mint_address: '0x1A1e5AC88C493e0608C84c60b7bb5f04D9cF50B3',
    nft_tx_hash: <'0x...'>,
    offline_deal: [ [Object], [Object], [Object], [Object], [Object] ]
  }, ...
]
```
