---
description: Mint NFT to MCS Opensea Collection
---

# Mint Assets as NFTs

`upload_nft_metadata(wallet_address, filename, nft_uri, tx_hash, file_size)`

`mint_nft(wallet_address, private_key, meta_url)`

The following code example mints an uploaded file as a NFT viewable on Opensea. Create an NFT object and provide the payload\_cid of the file. The NFT object follows the [Opensea metadata standards](https://docs.opensea.io/docs/metadata-standards).&#x20;

```
def test_mint_nft(wallet_info):
    wallet_address = wallet_info['wallet_address']
    private_key = wallet_info['private_key']
    web3_api = wallet_info['web3_api']
    
    w3_api = ContractAPI(web3_api)
    api = McsAPI()

    # upload file to mcs
    filepath = "/images/log_mcs.png"
    filename = "log_mcs.png"
    father_path = os.path.abspath(os.path.dirname(__file__))
    upload_file = api.upload_file(wallet_address, father_path + filepath)
    file_data = upload_file["data"]
    payload_cid, source_file_upload_id, nft_uri, file_size, w_cid = file_data['payload_cid'], file_data[
        'source_file_upload_id'], file_data['ipfs_url'], file_data['file_size'], file_data['w_cid']
    # get the global variable
    params = api.get_params()["data"]
    # get filcoin price
    rate = api.get_price_rate()["data"]
    # test upload_file_pay contract
    tx_hash = w3_api.upload_file_pay(wallet_address, private_key, 
        file_size, w_cid, rate, params)
    # upload nft metadata
    meta_url = api.upload_nft_metadata(wallet_address, filename, 
        nft_uri, tx_hash, file_size)['data']['ipfs_url']
    # test mint nft contract
    tx_hash, token_id = w3_api.mint_nft(wallet_address, private_key, meta_url)
```

{% embed url="https://github.com/filswan/nft" %}

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
