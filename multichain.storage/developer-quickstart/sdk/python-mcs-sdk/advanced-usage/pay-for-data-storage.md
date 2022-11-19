---
description: Pay for storage on MCS
---

# Pay for data storage

## Free Upload

Currently MCS have free upload amount 10GB for a wallet address every month. There is a 'status' in the MCS upload API response, which determines whether the current upload needs to be paid for. If the `'status'=="Free"`,  then the current deal will be processed without waiting for payment.

You can check if the current upload is free or not using a simple script:

{% code lineNumbers="true" %}
```python
need_pay = False
if file_data["status"] == "Free":
    self.upload_response = file_data
else:
    self.upload_response = file_data
    need_pay = True
```
{% endcode %}

## Approve Token

After a file is uploaded, the payment can be made through your wallet and the deal will be processed by MCS.&#x20;

To spend token, you need to first approve an amount for use (this amount have to be larger than the price for upload) or the smart contract will failed to process the payment.

`ContractAPI.approve_usdc(wallet_address, private_key, amount)`

First, we need to create an instance of ContractAPI class to access contract functions. Then we can approve a relative large amount that will guarantee the payment success.

{% code lineNumbers="true" %}
```python
w3_api = ContractAPI(web3_api)
w3_api.approve_usdc(wallet_address, private_key, 1)
```
{% endcode %}

## Get Estimate Amount

We can also get the estimate amount of the current upload. As a guide line of the amount to approve and potential cost for the current deal.

Let's get the file size from the response of the MCS upload API.

{% code lineNumbers="true" %}
```python
file_size = upload_file["data"]['file_size']
rate = self.api.get_price_rate()["data"]
amount = get_amount(file_size, rate)
print(amout)
```
{% endcode %}

## Payment

Then the payment can be executed using `file_size` and `w_cid`. Which can all be obtained from the response of upload API (or be accessed using file detail API that will be introduced later).

`ContractAPI.upload_file_pay(wallet_address, private_key, file_size, w_cid, rate, params)`

Let's use the return data from the upload\_file from previous upload examples.

{% code lineNumbers="true" %}
```python
file_data = upload_file["data"]
payload_cid, source_file_upload_id, nft_uri, file_size, w_cid = file_data['payload_cid'], file_data[
    'source_file_upload_id'], file_data['ipfs_url'], file_data['file_size'], file_data['w_cid']
    
# get the params for upload
params = api.get_params()["data"]
rate = api.get_price_rate()["data"]
    
# Transact the payment
w3_api.upload_file_pay(wallet_address, private_key, file_size, w_cid, rate, params)
```
{% endcode %}

### Parameters

* **wallet\_address**: the MetaMask wallet address.
* **private\_key**: wallet private key
* **file\_size:** the **** size of the uploaded file.
* **w\_cid**: unique payload CID of the file
* **params**: **** variables that can be obtained use API.
* **rate**: Filcoin price that can be obtained use API.

### Return

Returns a web3.py receipt object. In the example above, only the transaction hash from this object is printed.
