---
description: Guide to multichain.storage's onchain storage
---

# Onchain Storage

Onchain storage allows users to upload files to the IPFS server and backup into filecoin network.

### Upload File

`upload(file_path)`

Upload your file to IPFS and Filecoin network

```python
from swan_mcs import APIClient, OnchainAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
onchain_client = OnchainAPI(mcs_api, "<PRIVATE_KEY>", "<RPC_ENDPOINT>")

onchain_client.upload("<FILE_PATH>")
```

#### Parameters

* **file\_path**: The file path to upload

#### Return

```python
{
    "file_size": 1804,
    "ipfs_url": "https://ipfs.multichain.storage/ipfs/Qm...",
    "payload_cid": "Qm...",
    "source_file_upload_id": 151309,
    "status": "Pending",
    "w_cid": "a06...kYt"
}
```

### Pay for File Storage

`pay(source_file_upload_id, file_size)`

Pay for your file (in USDC) to be stored on the Filecoin network.

```python
from swan_mcs import APIClient, OnchainAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
onchain_client = OnchainAPI(mcs_api, "<PRIVATE_KEY>", "<RPC_ENDPOINT>")

onchain_client.pay("<SOURCE_FILE_UPLOAD_ID>", "<FILE_SIZE>")
```

#### Parameters

* **source\_file\_upload\_id**: The unique upload id of the file
* **file\_size**: the file size

#### Return

Returns the payment transaction hash

<pre class="language-python"><code class="lang-python"><strong>"0x..."
</strong></code></pre>

### Create NFT Collection

`create_collection(collection_metadata)`

Create your own NFT collection

```python
from swan_mcs import APIClient, OnchainAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
onchain_client = OnchainAPI(mcs_api, "<PRIVATE_KEY>", "<RPC_ENDPOINT>")

COLLECTION_DATA = {
    "name": '',
    "description": '',
    "image": '',
    "external_link": '',
    "seller_fee_basis_points": '',
    "fee_recipient": '' 
}

onchain_client.pay(COLLECTION_DATA)
```

#### Parameters

* **collection\_metadata**: A dictionary containing the metadata information of the collection

#### Return

Returns the created collection transaction hash and collection info

```python
{
    "name": '',
    "description": '',
    "image": '',
    "external_link": '',
    "seller_fee_basis_points": '',
    "fee_recipient": '' 
    "tx_hash": "0xA...",
}
```

### List NFT Collections

`get_collections()`

List all of your NFT Collections created on MCS

```python
from swan_mcs import APIClient, OnchainAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
onchain_client = OnchainAPI(mcs_api, "<PRIVATE_KEY>", "<RPC_ENDPOINT>")

for i in onchain_client.get_collections():
    print(i.to_json())
```

#### Return

Returns a list of Collection Objects

```python
{
    "address": "0x511...78e",
    "create_at": 1675178532,
    "description": null,
    "external_link": null,
    "id": 7,
    "image_url": "https://ipfs.multichain.storage/ipfs/Qm...",
    "is_default": true,
    "name": "Collection Name",
    "seller_fee": null,
    "tx_hash": null,
    "update_at": 1675178532,
    "wallet_id": null,
    "wallet_id_recipient": null,
    "wallet_recipient": ""
}
...
```

### Mint Assets as NFTs

`mint(source_file_upload_id, nft_object, collection_address='', quantity=1)`

```python
from swan_mcs import APIClient, OnchainAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
onchain_client = OnchainAPI(mcs_api, "<PRIVATE_KEY>", "<RPC_ENDPOINT>")

SOURCE_FILE_UPLOAD_ID = ''
NFT_OBJECT = {
    "name": "",
    "description": "",
    "image": ""
}
COLLECTION_ADDRESS = ''

onchain_client.pay(SOURCE_FILE_UPLOAD_ID, NFT_OBJECT, COLLECTION_ADDRESS)
```

#### Parameters

* **source\_file\_upload\_id**: The unique id of the file
* **nft\_object:** a python dictionary containing the nft information
* **collection\_address:** the collection address to mint to
* **quantity:** the quantity of tokens to mint (ERC-1155)&#x20;

#### Return

```python
{
    "hash": "0xA...",
    "tx_hash": "0xA...",
    "id": "##",
    "token_id": "##"
}
```
