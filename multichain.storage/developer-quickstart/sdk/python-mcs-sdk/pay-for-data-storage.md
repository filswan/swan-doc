---
description: Pay for storage on MCS
---

# Pay for data storage

After a file is uploaded, the file can be paid for by its cid (w\_cid). However, the wallet needs to be verified first, using `ContractAPI.approve_usdc(wallet_address, private_key, "1")`.

```
def test_approve_usdc(wallet_info):
    wallet_address = wallet_info['wallet_address']
    private_key = wallet_info['private_key']
    web3_api = wallet_info['web3_api']
    
    w3_api = ContractAPI(web3_api)
    w3_api.approve_usdc(wallet_address, private_key, "1")
```

### Parameters

* **wallet\_address**: the MetaMask wallet address.
* **private\_key**: wallet private key



Then the payment can be executed using `file_size` and `w_cid`. Which can all be obtained from the response of upload API (or be accessed using file detail API that will be introduced later).

`ContractAPI.upload_file_pay(wallet_address, private_key, file_size, w_cid, rate, params)`

```
def test_upload_file_pay(wallet_info):
    wallet_address = wallet_info['wallet_address']
    private_key = wallet_info['private_key']
    web3_api = wallet_info['web3_api']

    w3_api = ContractAPI(web3_api)
    api = McsAPI()
    # upload file to mcs
    file_path = "/*"
    upload_file = api.upload_file(wallet_address, file_path)
    file_data = upload_file["data"]
    payload_cid, source_file_upload_id, nft_uri, file_size, w_cid = file_data['payload_cid'], file_data[
        'source_file_upload_id'], file_data['ipfs_url'], file_data['file_size'], file_data['w_cid']
    # get the global variable
    params = api.get_params()["data"]
    # get filcoin price
    rate = api.get_price_rate()["data"]
    # upload_file_pay
    w3_api.upload_file_pay(wallet_address, private_key, file_size, w_cid, rate, params)
```

### Parameters

* **wallet\_address**: the MetaMask wallet address.
* **private\_key**: wallet private key
* **file\_size:** the **** size of the uploaded file.
* **w\_cid**: unique payload CID of the file
* **params**: **** variables that can be obtained use API.
* **rate**: Filcoin price that can be obtained use API.

### Return

Returns a web3.py receipt object. In the example above, only the transaction hash from this object is printed.
