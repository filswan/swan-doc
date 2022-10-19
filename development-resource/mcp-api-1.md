---
description: >-
  This is a Postman Collection for the Multi-Chain Storage API v1 endpoints. The
  page below describes different components of our API offering.
---

# MCS 2.0 API

## Authentication

{% swagger method="post" path="/api/v1/user/register" baseUrl="https://api.multichain.storage" summary="Register for Multichain storage" %}
{% swagger-description %}
Registration by Metamask wallet 
{% endswagger-description %}

{% swagger-parameter in="body" name="public_key_address" required="true" %}
Wallet address of the user
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status": "success",
    "data": {
        "nonce": "1086889515610840385225475684592216593766"
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/api/v1/user/login_by_metamask_signature" baseUrl="https://api.multichain.storage" summary=" Login for Multichain storage" %}
{% swagger-description %}
Login by signature via Metamask
{% endswagger-description %}

{% swagger-parameter in="body" name="nonce" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="signature" required="true" %}
Created by nonce, private key, and public key address.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="public_key_address" required="true" %}
Wallet address of the user
{% endswagger-parameter %}

{% swagger-parameter in="body" name="network" required="true" %}
Network for the chain environment 
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status": "success",
    "data": {
        "jwt_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2NjYyMjM3MDksImlhdCI6MTY2NjEzNzMwOSwic3ViIjoiNzExLHBvbHlnb24ubXVtYmFpIn0.SGu2DzoFcgNX9he_LHVUfQvfwM8rro_SsDXzH2imrKE"
    }
}
```
{% endswagger-response %}
{% endswagger %}

## Common

{% swagger method="get" path="/api/v1/common/system/params" baseUrl="https://api.multichain.storage" summary="Get system config" %}
{% swagger-description %}
This endpoint allows you to get system config
{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
<pre class="language-javascript"><code class="lang-javascript">{
    "data":
        "chain_name": "polygon.mainnet", 
<strong>        "payment_contract_address": "0xA1f32c758c4324cC3070A3AA107C4dC7DdFe1a6f",…}
</strong>        "chain_name": "polygon.mainnet"
        "dao_contract_address": "0x2621BB3140D8914806E977F7e6035B468675304D"
        "dao_threshold": 2
        "dex_address": "0x1b02dA8Cb0d097eB8D57A175b88c7D8b47997506"
        "filecoin_price": 513880000
        "gas_limit": 8000000
        "lock_time": 6
        "mint_contract_address": "0x7a5FB09Adc5f1bCd7bd1E230Dcc8B6d933c4995E"
        "pay_multiply_factor": 1.5
        "payment_contract_address": "0xA1f32c758c4324cC3070A3AA107C4dC7DdFe1a6f"
        "payment_recipient_address": "0x7042d0a8F7ED7d6051Fd7032515338f59Ff872b2"
        "usdc_address": "0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174"
<strong>        "usdc_wFil_pool_contract": "0x230e57B69E3d45557e20a6238462564EBf4Fe2a9"
</strong><strong>    "status": "success"
</strong>    }
}</code></pre>
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/api/v1/common/host/info" baseUrl="https://api.multichain.storage" summary="Get host info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status": "success",
    "data": {
        "version": "MCS-2.0.0",
        "operating_system": "darwin",
        "architecture": "arm64",
        "cpu_number": 8,
        "current_unix_nano": 1654203545105082000
    }
}
```
{% endswagger-response %}
{% endswagger %}

## Upload file

{% swagger method="get" path="/api/v1/billing/price/filecoin" baseUrl="https://api.multichain.storage" summary="Get USDC/Filecoin exchange rate" %}
{% swagger-description %}
This endpoint allows you to get the current exchange rate of USDC against Filecoin.
{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status":"success",
    "code":"200",
    "data":173
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/stats/storage" baseUrl="https://api.filswan.com" summary="Get average Filecoin statistics." %}
{% swagger-description %}
This endpoint allows you to get average Filecoin storage price.
{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
<pre class="language-javascript"><code class="lang-javascript">{
    "data":
    {
        "average_cost_push_message":" FIL",
        "average_data_cost_sealing_1TB":" FIL/TiB",
        "average_gas_cost_sealing_1TB":" FIL/TiB",
        "average_min_piece_size":" Byte",
        "average_price_per_GB_per_year":" FIL/GiB/year",
        "average_verified_price_per_GB_per_year":" FIL/GiB/year"},
        "historical_average_price_regular": " FIL/GiB/Day"
<strong>        "historical_average_price_verified": " FIL/GiB/Day"
</strong>    "status":"success"
}</code></pre>
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/api/v1/storage/ipfs/upload" baseUrl="https://api.multichain.storage" summary="Upload to IPFS" %}
{% swagger-description %}
This endpoint allows you to upload your file to IPFS server.
{% endswagger-description %}

{% swagger-parameter in="body" name="wallet_address" required="true" %}
wallet address used to pay
{% endswagger-parameter %}

{% swagger-parameter in="body" required="true" name="file" type="Binary" %}
file to be uploaded
{% endswagger-parameter %}

{% swagger-parameter in="body" name="duration" type="String" required="true" %}
days for the uploaded file to be kept on miner
{% endswagger-parameter %}

{% swagger-parameter in="body" name="file_type" required="true" %}
0:uploaded by user, 1:uploaded by nft
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
<pre class="language-javascript"><code class="lang-javascript">{
    "status": "success",
    "code": 200,
    "data": {
        "file_size": 2
        "ipfs_url": "https://ipfs.multichain.storage/ipfs/QmV9TXwuCutEUfcyMx4Ldk3MERubetXgCCkkE8QCHYyzL2"
        "payload_cid": "QmV9TXwuCutEUfcyMx4Ldk3MERubetXgCCkkE8QCHYyzL2"
<strong>        "source_file_upload_id": 150877
</strong><strong>        "status": "Free"
</strong><strong>        "w_cid": "1cdbc9a9-382a-4e53-9409-a0facb8fe31bQmV9TXwuCutEUfcyMx4Ldk3MERubetXgCCkkE8QCHYyzL2"
</strong>    }
}</code></pre>
{% endswagger-response %}
{% endswagger %}

## My files

{% swagger method="get" path="/api/v1/storage/tasks/deals" baseUrl="https://api.multichain.storage" summary="Get uploaded file list" %}
{% swagger-description %}
This endpoint allows you to get a list of your uploaded files.
{% endswagger-description %}

{% swagger-parameter in="path" name="wallet_address" required="true" %}
uploaded under this wallet
{% endswagger-parameter %}

{% swagger-parameter in="path" name="file_name" %}
file name of the uploaded file
{% endswagger-parameter %}

{% swagger-parameter in="path" name="page_size" type="Number" %}
valid integer, otherwise 10(default)
{% endswagger-parameter %}

{% swagger-parameter in="path" name="page_number" type="Number" %}
if not a valid number, or <=0, then 1, else use provided value
{% endswagger-parameter %}

{% swagger-parameter in="path" name="order_by" %}
file_name,file_size,upload_at(default)
{% endswagger-parameter %}

{% swagger-parameter in="path" name="is_ascend" %}
y:ascend, others: descend(default)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status": "success",
    "code": 200,
    "data": {
        "source_file_upload": [
            {
                "source_file_upload_id": 1,
                "car_file_id": 1,
                "file_name": "test20",
                "file_size": 1048671,
                "upload_at": 1651507047,
                "duration": 525,
                "pin_status": "Pinned",
                "payload_cid": "bafybeicxl5dk3iqejtbbcj2b77icx45unajw4qrakmd5ag46jlnidykk2y",
                "status": "Processing",
                "token_id": "",
                "mint_address": "",
                "nft_tx_hash": "",
                "offline_deal": [
                    {
                        "id": 1,
                        "car_file_id": 1,
                        "deal_cid": "bafyreihwmwh2jgapiube6wrviax2zolpe26w35w4wy2x6b7q6blff7mpwe",
                        "miner_id": 1,
                        "verified": false,
                        "start_epoch": 926524,
                        "sender_wallet_id": 1,
                        "deal_id": 167814,
                        "status": "Created",
                        "note": null,
                        "on_chain_status": "StorageDealError",
                        "tx_hash_unlock": null,
                        "unlock_at": 0,
                        "create_at": 1651507495,
                        "update_at": 1651516351,
                        "miner_fid": "t03354"
                    }
                ]
            },
            {
                "source_file_upload_id": 2,
                "car_file_id": 2,
                "file_name": "test20",
                "file_size": 1048671,
                "upload_at": 1651509153,
                "duration": 525,
                "pin_status": "Pinned",
                "payload_cid": "bafybeicxl5dk3iqejtbbcj2b77icx45unajw4qrakmd5ag46jlnidykk2y",
                "status": "Processing",
                "token_id": "",
                "mint_address": "",
                "nft_tx_hash": "",
                "offline_deal": [
                    {
                        "id": 2,
                        "car_file_id": 2,
                        "deal_cid": "bafyreic6dd722zindqx6svw4snk5czwn4hi4dprzcps3xkiiklqrz5ay5a",
                        "miner_id": 1,
                        "verified": false,
                        "start_epoch": 926588,
                        "sender_wallet_id": 1,
                        "deal_id": 167815,
                        "status": "Created",
                        "note": null,
                        "on_chain_status": "StorageDealError",
                        "tx_hash_unlock": null,
                        "unlock_at": 0,
                        "create_at": 1651509304,
                        "update_at": 1651516351,
                        "miner_fid": "t03354"
                    }
                ]
            },
            {
                "source_file_upload_id": 3,
                "car_file_id": 0,
                "file_name": "test20",
                "file_size": 1048671,
                "upload_at": 1651516702,
                "duration": 525,
                "pin_status": "Pinned",
                "payload_cid": "",
                "status": "Pending",
                "token_id": "",
                "mint_address": "",
                "nft_tx_hash": "",
                "offline_deal": []
            },
            {
                "source_file_upload_id": 4,
                "car_file_id": 0,
                "file_name": "test20",
                "file_size": 1048671,
                "upload_at": 1651519341,
                "duration": 525,
                "pin_status": "Pinned",
                "payload_cid": "",
                "status": "Pending",
                "token_id": "",
                "mint_address": "",
                "nft_tx_hash": "",
                "offline_deal": []
            }
        ],
        "total_record_count": 4
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/api/v1/storage/deal/detail/<deal_id>" baseUrl="https://api.multichain.storage" summary="Get deal details" %}
{% swagger-description %}
This endpoint allows you to get deal details and DAO details.
{% endswagger-description %}

{% swagger-parameter in="path" name="source_file_upload_id" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status": "success",
    "code": 200,
    "data": {
        "dao_threshold": 2,
        "source_file_upload_deal": {
            "deal_id": 0,
            "deal_cid": "",
            "message_cid": "",
            "height": 0,
            "piece_cid": "",
            "verified_deal": false,
            "storage_price_per_epoch": 0,
            "signature": "",
            "signature_type": "",
            "created_at": 0,
            "piece_size_format": "",
            "start_height": 0,
            "end_height": 0,
            "client": "",
            "client_collateral_format": "",
            "provider": "",
            "provider_tag": "",
            "verified_provider": 0,
            "provider_collateral_format": "",
            "status": 0,
            "network_name": "",
            "storage_price": 0,
            "ipfs_url": "http://192.168.88.41:5050/ipfs/QmeHeqoByW6dGSba9joVUiPuyVafTm5m1qsEtRcYBmjtdr",
            "file_name": "test20",
            "w_cid": "cff75975-144c-4e10-a1d7-ae0c30c1365cQmeHeqoByW6dGSba9joVUiPuyVafTm5m1qsEtRcYBmjtdr",
            "locked_at": 1651507068,
            "locked_fee": "5364546000000000",
            "unlocked": false
        }
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/api/v1/storage/deal/log/<offline_deal_id>" baseUrl="https://api.multichain.storage" summary="get deal logs" %}
{% swagger-description %}
This endpoint allows you to get offline deal logs
{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status": "success",
    "code": 200,
    "data": {
        "offline_deal_log": [
            {
                "id": 1,
                "offline_deal_id": 1,
                "on_chain_status": "StorageDealCheckForAcceptance",
                "on_chain_message": "Provider state: StorageDealWaitingForData",
                "create_at": 1651507615
            },
            {
                "id": 2,
                "offline_deal_id": 1,
                "on_chain_status": "StorageDealCheckForAcceptance",
                "on_chain_message": "Provider state: StorageDealPublish",
                "create_at": 1651507915
            },
            {
                "id": 3,
                "offline_deal_id": 1,
                "on_chain_status": "StorageDealCheckForAcceptance",
                "on_chain_message": "Provider state: StorageDealUnknown",
                "create_at": 1651509124
            }
        ]
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/api/v1/billing/deal/lockpayment/info" baseUrl="https://api.multichain.storage" summary="Get payment information" %}
{% swagger-description %}
This endpoint allows you to get the specific payment information by payload CID.
{% endswagger-description %}

{% swagger-parameter in="path" name="source_file_upload_id" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status": "success",
    "code": 200,
    "data": {
        "w_cid": "cff75975-144c-4e10-a1d7-ae0c30c1365cQmeHeqoByW6dGSba9joVUiPuyVafTm5m1qsEtRcYBmjtdr",
        "pay_amount": "5364546000000000",
        "pay_tx_hash": "0x864cb80257ea9e51d8ac8bedbd367d69b8effd7278db845d72c38a45b68f5fed",
        "token_address": "0xe11A86849d99F524cAC3E7A0Ec1241828e332C62"
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/api/v1/storage/mint/info" baseUrl="https://api.multichain.storage" summary="Record mint info" %}
{% swagger-description %}
This endpoint allows to record mint info to mcs database.
{% endswagger-description %}

{% swagger-parameter in="body" name="source_file_upload_id" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="tx_hash" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="token_id" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="mint_address" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status": "success",
    "code": 200,
    "data": {
        "id": 1,
        "source_file_upload_id": 1,
        "nft_tx_hash": "ab",
        "mint_address": "eee",
        "token_id": "e",
        "create_at": 1651502337,
        "update_at": 1651502337
    }
}
```
{% endswagger-response %}
{% endswagger %}

## Billing history

{% swagger method="get" path="/api/v1/billing" baseUrl="https://mcs-api.filswan.com" summary="Get billing history" %}
{% swagger-description %}
This endpoint allows you to get the billing history related to current wallet account.
{% endswagger-description %}

{% swagger-parameter in="path" name="wallet_address" required="true" type="String" %}
wallet who pay the file
{% endswagger-parameter %}

{% swagger-parameter in="path" name="page_size" type="Number" %}
valid integer, otherwise 10(default)
{% endswagger-parameter %}

{% swagger-parameter in="path" name="page_number" type="Number" %}
valid integer, otherwise 1(default)
{% endswagger-parameter %}

{% swagger-parameter in="path" name="file_name" %}
file whose file_name include the parameter
{% endswagger-parameter %}

{% swagger-parameter in="path" name="order_by" %}
pay_amount,unlock_amount,file_name,pay_at(default),unlock_at,deadline
{% endswagger-parameter %}

{% swagger-parameter in="path" name="is_ascend" %}
y:ascend, others: descend(default)
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status": "success",
    "code": 200,
    "data": {
        "billing": [
            {
                "pay_id": 1,
                "pay_tx_hash": "0x864cb80257ea9e51d8ac8bedbd367d69b8effd7278db845d72c38a45b68f5fed",
                "pay_amount": "5364546000000000",
                "unlock_amount": "",
                "file_name": "test20",
                "payload_cid": "bafybeicxl5dk3iqejtbbcj2b77icx45unajw4qrakmd5ag46jlnidykk2y",
                "pay_at": 1651507068,
                "unlock_at": 0,
                "deadline": 1652025461,
                "network_name": "polygon.mainnet",
                "token_name": "USDC"
            },
            {
                "pay_id": 2,
                "pay_tx_hash": "0x9d0bd6698230aadfd1c8fafe34db730385173fddeed1275f3c3a93563b16f8c5",
                "pay_amount": "5364546000000000",
                "unlock_amount": "",
                "file_name": "test20",
                "payload_cid": "bafybeicxl5dk3iqejtbbcj2b77icx45unajw4qrakmd5ag46jlnidykk2y",
                "pay_at": 1651509167,
                "unlock_at": 0,
                "deadline": 1652027565,
                "network_name": "polygon.mainnet",
                "token_name": "USDC"
            }
        ],
        "total_record_count": 2
    }
}
```
{% endswagger-response %}
{% endswagger %}
