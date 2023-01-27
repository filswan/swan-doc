---
description: Demo for using MCS simple upload
---

# Simple Upload

## Writing SDK Scripts

To begin writing a script utilizing the SDK, create a new `.py` file. Let's create a file named `test.py` for this guide.

At the top of this file, `import` the OnchainUpload class from python MCS SDK packages for the script.

{% code lineNumbers="true" %}
```python
from mcs.upload.onchain_upload import OnchainUpload
```
{% endcode %}

Now we can begin writing the demo script.

### Load Wallet Information

Add your wallet info and&#x20;

<pre class="language-python"><code class="lang-python"><strong>if __name__ == "__main__"    
</strong><strong>    private_key="&#x3C;PRIVATE_KEY>"
</strong>    rpc_endpoint="&#x3C;RPC_ENDPOINT>"
    api_key = "&#x3C;API_KEY>"
    access_token = "&#x3C;ACCESS_TOKEN>"
</code></pre>

{% hint style="info" %}
You can use other methods to securely store your wallet information!
{% endhint %}

#### Guide for load wallet information with .env

{% content-ref url="advanced-usage/load-dotenv.md" %}
[load-dotenv.md](advanced-usage/load-dotenv.md)
{% endcontent-ref %}

### Initialize Upload

To start an upload, we need to create an instance of the `MCSUpload` class. Which requires `chain_name`, `wallet_address`, `private_key` and `file_path` as parameters. The upload process requires the user login into the MCS API using a wallet address. Python MCS SDK can handle this process automatically when initializing an MCSUpload.

```python
    # Use absolute path or relative path to the current directory.
    file_path = "<file_path>"
    
    upload_handle = OnchainUpload('polygon.mainnet', private_key, \
            rpc_endpoint, api_key, access_token, file_path)
```

### Simple Upload File

To use the fastest way to upload the file to [multichain.storage](https://multichain.storage), we need to call the `simple_upload()` function.

```python
    # Use the amount token to approve (integer) as parameter
    hash = upload_handle.simple_upload(<amount_token_to_approve>)
```

The amount of tokens to approve is the amount of USDC to be approved through the Swan payment contract. You need to approve a sufficient amount to upload successfully.

### Mint NFT

You can mint your upload to OpenSea as NFT through SwanMint smart contract.

```python
    upload_handle.mint('<NFT_name>')
```

## Full Demo Code

```python
from mcs.upload.onchain_upload import OnchainUpload

if __name__ == "__main__":  
    private_key="<PRIVATE_KEY>"
    rpc_endpoint="<RPC_ENDPOINT>"
    api_key = "<API_KEY>"
    access_token = "<ACCESS_TOKEN>"
    
    filepath = "<file_path>"
    upload_handle = OnchainUpload('polygon.mainnet', private_key, \
            rpc_endpoint, api_key, access_token, filepath)
    hash = upload_handle.simple_upload(<APPROVE_AMOUNT>)
```
