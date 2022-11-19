---
description: Demo for using MCS simple upload
---

# Simple Upload

## Writing SDK Scripts

To begin writing a script utilizing the SDK, create a new `.py` file. Let's create a file named `test.py` for this guide.

At the top of this file, `import` the necessary packages for the script.

{% code lineNumbers="true" %}
```python
import os
from mcs import McsAPI
from dotenv import load_dotenv
```
{% endcode %}

Now we can begin writing the demo script.

### Load Wallet Information

Create an `.env` file

```
wallet_address="<WALLET_ADDRESS>"
private_key="<PRIVATE_KEY>"
rpc_endpoint="<RPC_ENDPOINT>"
```

Install python-dotenv

```
pip install python-dotenv
```

{% hint style="info" %}
You can use other methods to secure your wallet information!
{% endhint %}

### Initialize Upload

To start an upload, we need to create an instance of the `MCSUpload` class. Which requires `chain_name`, `wallet_address`, `private_key` and `file_path` as parameters. The upload process requires the user login into the MCS API using a wallet address. Python MCS SDK can handle this process automatically when initializing an MCSUpload.

```python
import os
from mcs import McsAPI
from dotenv import load_dotenv

load_dotenv(".env")
file_path="./test.py"
upload_handle = MCSUpload("polygon.mainnet", os.getenv('wallet_address'), \
    os.getenv('private_key'), os.getenv('rpc_endpoint'), file_path)
```

### Upload File

To upload the file to [multichain.storage](https://multichain.storage), we need to call the `stream_upload()` function.

```python
file_data, need_pay = upload_handle.stream_upload()
```

The upload function uploads the file to the IPFS server. MCS currently has 10GB of free upload per month for each wallet. The `need_pay` will indicates if a file is under the coverage of free upload. When `need_pay == 1` then the file needs to be paid and it is free when `need_pay == 0`.

### Approve Token

Before processing payment we need to approve enough tokens for the upload payment and gas fee. You don't need to approve any token if the upload is free. You can also choose how much you want to approve based on the estimated price.

```python
upload_handle.approve_token(<amount>)
```

### Estimate Payment

The estimated payment can be accessed using the `estimate_amount()` function.

```python
print(upload_handle.estimate_amount())
```

### Payment

Currently, on MCS mainnet, users only need to pay if the upload surpasses the free upload coverage. However, users can still force a payment after upload (This is not recommended).

```python
if need_pay:
  upload_handle.pay()
```
