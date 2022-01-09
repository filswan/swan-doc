---
description: >-
  This is a Postman Collection for the Multi-Chain Payment API v1 endpoints. The
  page below describes different components of our API offering.
---

# MCP API

## Config

{% swagger method="get" path="/api/v1/common/system/params" baseUrl="https://calibration-mcp-api.filswan.com" summary="Get system config" %}
{% swagger-description %}
This endpoint allows you to get system config
{% endswagger-description %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status": "success",
    "code": "200",
    "data": {
        "LOCK_TIME": "6",
        "PAY_GAS_LIMIT": "9999999",
        "PAY_WITH_MULTIPLY_FACTOR": "1.5",
        "RECIPIENT": "",
        "SWAN_PAYMENT_CONTRACT_ADDRESS": "",
        "USDC_ADDRESS": ""
    }
}
```
{% endswagger-response %}
{% endswagger %}

## Upload file

{% swagger method="get" path="/api/v1/billing/price/filecoin" baseUrl="https://calibration-mcp-api.filswan.com" summary="Get USDC/Filecoin exchange rate" %}
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

{% swagger method="get" path="/stats/storage" baseUrl="https://calibration-api.filswan.com" summary="Get average Filecoin statistics." %}
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

{% swagger method="post" path="/api/v1/storage/ipfs/upload" baseUrl="https://calibration-mcp-api.filswan.com" summary="Upload to IPFS" %}
{% swagger-description %}
This endpoint allows you to upload your file to IPFS server.
{% endswagger-description %}

{% swagger-parameter in="body" required="true" name="file" type="Binary" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="duration" type="Number" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    "status":"success",
    "code":"200",
    "data":{
        "payload_cid":"",
        "ipfs_url":"",
        "need_pay":0
    }
}
```
{% endswagger-response %}
{% endswagger %}

## My files

{% swagger method="get" path="/api/v1/storage/tasks/deals" baseUrl="https://calibration-mcp-api.filswan.com" summary="Get uploaded file list" %}
{% swagger-description %}
This endpoint allows you to get a list of your uploaded files.
{% endswagger-description %}

{% swagger-parameter in="path" name="file_name" %}

{% endswagger-parameter %}

{% swagger-parameter in="path" name="page_size" type="Number" %}

{% endswagger-parameter %}

{% swagger-parameter in="path" name="page_number" type="Number" %}

{% endswagger-parameter %}

{% swagger-parameter in="path" name="source_id" required="true" type="Number" %}

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

{% swagger method="get" path="/api/v1/storage/deal/detail/<deal_id>" baseUrl="https://calibration-mcp-api.filswan.com" summary="Get deal details" %}
{% swagger-description %}
This endpoint allows you to get deal details and DAO details.
{% endswagger-description %}

{% swagger-parameter in="path" name="payload_cid" required="true" %}

{% endswagger-parameter %}
{% endswagger %}

{% swagger method="get" path="/api/v1/billing/deal/lockpayment/info" baseUrl="https://calibration-mcp-api.filswan.com" summary="Get payment information" %}
{% swagger-description %}
This endpoint allows you to get the specific payment information by payload CID.
{% endswagger-description %}

{% swagger-parameter in="path" name="payload_cid" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="path" name="wallet_address" required="true" %}

{% endswagger-parameter %}
{% endswagger %}

## Billing history

{% swagger method="get" path="/api/v1/billing" baseUrl="https://calibration-mcp-api.filswan.com" summary="Get billing history" %}
{% swagger-description %}
This endpoint allows you to get the billing history related to current wallet account.
{% endswagger-description %}

{% swagger-parameter in="path" name="wallet_address" required="true" %}

{% endswagger-parameter %}

{% swagger-parameter in="path" name="tx_hash" %}

{% endswagger-parameter %}

{% swagger-parameter in="path" name="page_size" type="Number" %}

{% endswagger-parameter %}

{% swagger-parameter in="path" name="page_number" type="Number" %}

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
