---
description: >-
  This is a Postman Collection for the Multi-Chain Storage API v1 endpoints. The
  page below describes different components of our API offering.
---

# MCS API

## Common

{% swagger method="get" path="/api/v1/common/system/params" baseUrl="https://mcs-api.filswan.com" summary="Get system config" %}
{% swagger-description %}
This endpoint allows you to get system config
{% endswagger-description %}

{% swagger-parameter in="path" name="limit" %}
When not provided, use default: 100
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status": "success",
    "code": "200",
    "data": {
        "LOCK_TIME": "6",
        "MINT_CONTRACT": "0x1A1e5AC88C493e0608C84c60b7bb5f04D9cF50B3",
        "PAY_GAS_LIMIT": "9999999",
        "PAY_WITH_MULTIPLY_FACTOR": "1.5",
        "RECIPIENT": "0xABeAAb124e6b52afFF504DB71bbF08D0A768D053",
        "SWAN_PAYMENT_CONTRACT_ADDRESS": "0x7ab09f9Ab4D39cfBE0551dfb6AdAc63C89bB955b",
        "USDC_ADDRESS": "0xe11A86849d99F524cAC3E7A0Ec1241828e332C62"
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/api/v1/common/host/info" baseUrl="https://mcs-api.filswan.com" summary="Get host info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
```javascript
{{
    "status": "success",
    "code": "200",
    "data": {
        "swan_miner_version": "swan-miner-v2.5.0",
        "operating_system": "linux",
        "architecture": "amd64",
        "cpu_number": 8
    }
}
```
{% endswagger-response %}
{% endswagger %}

## Upload file

{% swagger method="get" path="/api/v1/billing/price/filecoin" baseUrl="https://mcs-api.filswan.com" summary="Get USDC/Filecoin exchange rate" %}
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
```javascript
{
    "data":
    {
        "average_cost_push_message":" FIL",
        "average_data_cost_sealing_1TB":" FIL/TiB",
        "average_gas_cost_sealing_1TB":" FIL/TiB",
        "average_min_piece_size":" Byte",
        "average_price_per_GB_per_year":" FIL/GiB/year",
        "average_verified_price_per_GB_per_year":" FIL/GiB/year"},
        "status":"success"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/api/v1/storage/ipfs/upload" baseUrl="https://mcs-api.filswan.com" summary="Upload to IPFS" %}
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
```javascript
{
    "status": "success",
    "code": "200",
    "data": {
        "source_file_id": 593,
        "payload_cid": "bafykbzacecjq3txd5liqtv52cmguj6mmx7uwhdhb6cfxlgv53ytk4xk5osyvg",
        "ipfs_url": "https://calibration-ipfs.filswan.com/ipfs/QmdJGnSpXCX9zGEh1G9RwBRUH1KYhtNqsZH1ZdXRQidXWR",
        "need_pay": 0,
        "file_size": 2504638
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/api/v1/storage/ipfs/batchupload" baseUrl="https://mcs-api.filswan.com" summary="Batch Upload to IPFS" %}
{% swagger-description %}
This endpoint allows you to batch upload your file to IPFS server.
{% endswagger-description %}

{% swagger-parameter in="body" name="wallet_address" required="true" %}
wallet address used to pay
{% endswagger-parameter %}

{% swagger-parameter in="body" name="files" type="Binary" required="true" %}
file to be uploaded
{% endswagger-parameter %}

{% swagger-parameter in="body" required="true" name="duration" %}
days for the uploaded file to be kept on miner
{% endswagger-parameter %}

{% swagger-parameter in="body" name="file_type" required="true" %}
0:uploaded by user, 1:uploaded by nft
{% endswagger-parameter %}
{% endswagger %}

## My files

{% swagger method="get" path="/api/v1/storage/tasks/deals" baseUrl="https://mcs-api.filswan.com" summary="Get uploaded file list" %}
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
upper limit or records to return this time
{% endswagger-parameter %}

{% swagger-parameter in="path" name="page_number" type="Number" %}
if not a valid number, or <=0, then 1, else use provided value
{% endswagger-parameter %}

{% swagger-parameter in="path" required="false" name="payload_cid" %}
payload cid of the car file for uploaded file
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    code: "200"
    data: 
    [
        {
            id: 0, 
            user_id:, 
            file_name: "", 
            file_size: "",…
        },…
    ]
    page_info: 
    {
        page_number: "1", 
        page_size: "10", 
        total_record_count: ""
    }
    status: "success"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/api/v1/storage/deal/detail/<deal_id>" baseUrl="https://mcs-api.filswan.com" summary="Get deal details" %}
{% swagger-description %}
This endpoint allows you to get deal details and DAO details.
{% endswagger-description %}

{% swagger-parameter in="path" name="payload_cid" required="true" %}
payload cid of the car file for uploaded file
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status": "success",
    "code": "200",
    "data": {
        "dao": [
            {
                "dao_name": "Dao2",
                "dao_address": "0x6f2B76024196e82D81c8bC5eDe7cff0B0276c9C1",
                "order_index": "2",
                "deal_id": 4813917,
                "dao_pass_time": "1648074606",
                "payload_cid": "bafykbzacedp5sm4hgjc5l5d3hadkjw7t6dz6qtkyug4kdb7vyojlgwojuhr32",
                "dao_address_event": "0x6f2B76024196e82D81c8bC5eDe7cff0B0276c9C1",
                "tx_hash": "0x38d63b594193ecc568219f73ed138f152ebcb76e1b3e821acb20eb4cc18702d8",
                "status": "1"
            },
            {
                "dao_name": "Dao3",
                "dao_address": "0x800210CfB747992790245eA878D32F188d01a03A",
                "order_index": "3",
                "deal_id": 4813917,
                "dao_pass_time": "1648074636",
                "payload_cid": "bafykbzacedp5sm4hgjc5l5d3hadkjw7t6dz6qtkyug4kdb7vyojlgwojuhr32",
                "dao_address_event": "0x800210CfB747992790245eA878D32F188d01a03A",
                "tx_hash": "0x4db5ffcac1231a4a10b8cfb926e2273f47ac0f6998db8f419d40da56ee249b2d",
                "status": "1"
            },
            {
                "dao_name": "Dao1",
                "dao_address": "0x05856015d07F3E24936B7D20cB3CcfCa3D34B41d",
                "order_index": "1",
                "deal_id": 0,
                "dao_pass_time": "",
                "payload_cid": "",
                "dao_address_event": "",
                "tx_hash": "",
                "status": ""
            }
        ],
        "dao_thresh_hold": 2,
        "dao_total_count": 3,
        "deal": {
            "deal_id": 4813917,
            "deal_cid": "bafyreiha2opmhanchdezyynfwbnbgvfhsd7l6al6r32tjgzovwews75fba",
            "message_cid": "bafy2bzacedwh5otlxmyyruk3k6hue4dm6qhegvuisv7tjib37wnlgllqf26ec",
            "height": 1658913,
            "piece_cid": "baga6ea4seaqeqjfpuk76spigclf5hti2v3tia2mz4pyomxxnkegcdzhlcge4agi",
            "verified_deal": true,
            "storage_price_per_epoch": 0,
            "signature": "",
            "signature_type": "",
            "created_at": 1648073790,
            "piece_size_format": "",
            "start_height": 1669905,
            "end_height": 3184293,
            "client": "f14r2jybmccwiu6hze4fu55jyhclktvwacec56hea",
            "client_collateral_format": "000000000000000000",
            "provider": "f019104",
            "provider_tag": "",
            "verified_provider": 0,
            "provider_collateral_format": "000000000000000000",
            "status": 0,
            "network_name": "filecoin_mainnet",
            "storage_price": 0,
            "ipfs_url": "https://calibration-ipfs.filswan.com/ipfs/QmP6TY2Nm1BJmQsypnUYbfSe1sQ8KpEU2DpSVP8T9siTFC",
            "file_name": "instruction148.docx"
        },
        "found": {
            "payload_cid": "bafykbzacedp5sm4hgjc5l5d3hadkjw7t6dz6qtkyug4kdb7vyojlgwojuhr32",
            "client_wallet_address": "",
            "create_at": "1648054345164",
            "locked_fee": "263721000000000"
        },
        "signed_dao_count": 2,
        "unlock_status": true
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/api/v1/storage/deal/log/<deal_cid>" baseUrl="https://mcs-api.filswan.com" summary="get deal logs" %}
{% swagger-description %}
This endpoint allows you to get offline deal logs
{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status": "success",
    "code": "200",
    "data": {
        "offline_deal_logs": [
            {
                "id": 57,
                "deal_cid": "bafyreic7izff2iezvpgepliv2mfrzhdcmxixx2w637kprg6p3f7uvoaefe",
                "status": "StorageDealActive",
                "message": "",
                "create_at": "1646998800016"
            },
            {
                "id": 49,
                "deal_cid": "bafyreic7izff2iezvpgepliv2mfrzhdcmxixx2w637kprg6p3f7uvoaefe",
                "status": "StorageDealAwaitingPreCommit",
                "message": "",
                "create_at": "1646968320019"
            },
            {
                "id": 48,
                "deal_cid": "bafyreic7izff2iezvpgepliv2mfrzhdcmxixx2w637kprg6p3f7uvoaefe",
                "status": "StorageDealCheckForAcceptance",
                "message": "Provider state: StorageDealPublishing",
                "create_at": "1646968080008"
            },
            {
                "id": 47,
                "deal_cid": "bafyreic7izff2iezvpgepliv2mfrzhdcmxixx2w637kprg6p3f7uvoaefe",
                "status": "StorageDealCheckForAcceptance",
                "message": "Provider state: StorageDealPublish",
                "create_at": "1646967360012"
            },
            {
                "id": 46,
                "deal_cid": "bafyreic7izff2iezvpgepliv2mfrzhdcmxixx2w637kprg6p3f7uvoaefe",
                "status": "StorageDealCheckForAcceptance",
                "message": "Provider state: StorageDealWaitingForData",
                "create_at": "1646966400009"
            }
        ]
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/api/v1/billing/deal/lockpayment/info" baseUrl="https://mcs-api.filswan.com" summary="Get payment information" %}
{% swagger-description %}
This endpoint allows you to get the specific payment information by payload CID.
{% endswagger-description %}

{% swagger-parameter in="path" name="payload_cid" required="true" %}
payload cid of the car file for the source file
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status": "success",
    "code": "200",
    "data": {
        "locked_fee": "7283883000000000",
        "payload_cid": "bafykbzacebk3f4v4cqdfch35h3arwelg4hodutkahwa45nrnpbadui7uzaky6",
        "tx_hash": "0xe53608744eac42fcc784d4ba8cef151583c33ff3b8f42424166867be25305f7f"
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/api/v1/storage/mint/info" baseUrl="https://mcs-api.filswan.com" summary="Record mint info" %}
{% swagger-description %}
This endpoint allows to record mint info to mcs database.
{% endswagger-description %}

{% swagger-parameter in="body" name="payload_cid" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="tx_hash" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="token_id" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="mint_address" required="true" %}

{% endswagger-parameter %}
{% endswagger %}

## Billing history

{% swagger method="get" path="/api/v1/billing" baseUrl="https://mcs-api.filswan.com" summary="Get billing history" %}
{% swagger-description %}
This endpoint allows you to get the billing history related to current wallet account.
{% endswagger-description %}

{% swagger-parameter in="path" name="wallet_address" required="true" type="String" %}
wallet who pay the file
{% endswagger-parameter %}

{% swagger-parameter in="path" name="tx_hash" %}
transaction hash of payment
{% endswagger-parameter %}

{% swagger-parameter in="path" name="page_size" type="Number" %}
when empty, use default:10, max records returned each time
{% endswagger-parameter %}

{% swagger-parameter in="path" name="page_number" type="Number" %}
when empty string, then 1
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    code: "200"
    data: 
    [
        {
            tx_hash: "",…
        }
    ]
    page_info: 
    {
        page_number: "1", 
        page_size: "10", 
        total_record_count: ""
    }
    status: "success"    
}
```
{% endswagger-response %}
{% endswagger %}
