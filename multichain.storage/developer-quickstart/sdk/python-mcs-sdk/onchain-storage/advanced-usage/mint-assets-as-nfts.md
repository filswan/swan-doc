---
description: Mint NFT to MCS Opensea Collection
---

# Mint Assets as NFTs

`McsAPI.upload_nft_metadata(wallet_address, filename, nft_uri, tx_hash, file_size)`

`ContractAPI.mint_nft(wallet_address, private_key, meta_url)`

The following code example mints an uploaded file as a NFT viewable on Opensea. Create an NFT object and provide the payload\_cid of the file. The NFT object follows the [Opensea metadata standards](https://docs.opensea.io/docs/metadata-standards).&#x20;

{% code lineNumbers="true" %}
```python
meta_url = onchain_api.upload_nft_metadata(wallet_address, filename, 
    nft_uri, tx_hash, file_size)['data']['ipfs_url']
# mint nft contract
tx_hash, token_id = w3_api.mint_nft(wallet_address, private_key, meta_url)
# update mint info
onchain_api.get_mint_info(source_file_upload_id, None, tx_hash, token_id, wallet_address)
```
{% endcode %}

### Parameters

* **wallet\_address**: the MetaMask wallet address.
* **private\_key**: wallet private key
* **meta\_url**: can be obtained through `upload_nft_metadata`

### Return

Returns the response from the `/mint/info` API

```
{
  status: 'success',
  data: {
    id: <ID>,
    source_file_upload_id: <ID>,
    nft_tx_hash: <'0x...'>,
    mint_address: '0x1A1e5AC88C493e0608C84c60b7bb5f04D9cF50B3',
    token_id: '<ID>',
    create_at: <TIME>,
    update_at: <TIME>
  }
}
```
