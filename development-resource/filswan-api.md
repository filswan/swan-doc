---
description: >-
  This is a Postman Collection for the FilSwan API v2 endpoints. The page below
  describes different components of our API offering.
---

# FilSwan API

## Authorization

These endpoints return details about Authorization.

{% swagger baseUrl="https://api.filswan.com" path="/auth/login" method="post" summary="Get Auth Token" %}
{% swagger-description %}
This endpoint allows you to get an JWT Bearer Token (auth_token) from email and password. 

\


The auth_token can be used for generate other API Keys.
{% endswagger-description %}

{% swagger-parameter in="body" name="email" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="password" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "auth_token": "eyJ0eXAiOiJKV1QiLCJhbGci1iJIUzI1NiJ9.eyJleHAi5jE2XTM4NDY2ODUsImlhdCI6MTYxMzc2MDI4NSwic3ViIjoxODB9.nqVR7pZ5voIEotp85zA2dEzIEmAMbiWcCBkvT06ILu4",
  "message": "Successfully logged in.",
  "status": "success"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://api.filswan.com" path="/user/api_keys/jwt" method="post" summary="Generate API Key" %}
{% swagger-description %}
This endpoint allows you to issue new API keys for their account programmatically. The only key-type that can be used to issue new keys is the login user's JWT Bearer Token.

\


The purpose of this endpoint is to allow for programmatic creation of API keys that may be used for multiple projects, individual users, or a variety of other use cases where a single API key pair across an account is not sufficient.

\


This endpoint will return three values: The API Key, the API Secrect, and a JWT Bearer Token. Make sure to record the API Secret and the JWT as they will not be accessible again.
{% endswagger-description %}

{% swagger-parameter in="body" name="key_name" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "auth_token": {
    "access_token": "6ca9a6575b7255b3f15xxxxxxxxxxx17a1",
    "apikey": "7WIhxxxxxxxxxx0YSmGw",
    "created_on": "1614229867",
    "jwt": "eyJ0eXAiOiJxxxxxxxxxxxOiJIUzI1NiJ9.eyJleHAiOjExxxxxxxxxxxxDIyOTg2Nywic3ViIjoiN1dJaGM5bkNrR1gzVk9VczBZU21HdyJ9.CO5oXVnDGcTwxxxxxxxI6xC5IBF2NdJkt34",
    "key_name": "test",
    "status": "Created"
  },
  "message": "api token successfully created.",
  "status": "success"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://api.filswan.com" path="/user/api_keys/jwt" method="post" summary="Generate JWT token" %}
{% swagger-description %}
To use the bearer authentication model, you will need the JWT that is generated using this API.

\


This token can be used as an Authorization header for all your API requests in the following format: "Authorization": "Bearer YOUR_JWT"
{% endswagger-description %}

{% swagger-parameter in="body" name="access_token" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="apikey" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "data": {
    "api_key": "my-apikey-name",
    "jwt": "my-api-token"
  },
  "status": "success"
}
```
{% endswagger-response %}
{% endswagger %}

## Miners

These endpoints return details about storage providers specified by the requested IDs.

{% swagger baseUrl="https://api.filswan.com" path="/miners?limit={{limit}}&offset={{offset}}&location={{location}}&offline_deal_available={{offline_deal_available}}&status={{status}}&sort_by={{sort_by}}&order={{order}}" method="get" summary="List Storager Provider" %}
{% swagger-description %}
This endpoint allows you to get a list of storage providers.
{% endswagger-description %}

{% swagger-parameter in="path" name="limit" type="integer" %}
Number of items in one page. Default: 10
{% endswagger-parameter %}

{% swagger-parameter in="path" name="offset" type="integer" %}
Page number, starts from 0. Default: 0
{% endswagger-parameter %}

{% swagger-parameter in="path" name="location" type="string" %}
The location of miners. If empty, it shows miners at all locations. Possible values: Global, Asia, Africa, North America, South America, Europe, Oceania
{% endswagger-parameter %}

{% swagger-parameter in="path" name="offline_deal_available" type="integer" %}
Miner accept offline deals or not. If empty, it shows all miners. Possible values: 1, 0
{% endswagger-parameter %}

{% swagger-parameter in="path" name="status" type="string" %}
The status of miners. If empty, it shows all miners in any status. Possible values: Active, Offline.
{% endswagger-parameter %}

{% swagger-parameter in="path" name="sort_by" type="string" %}
Possible values: update_time_str, price, verified_price, score, status, location
{% endswagger-parameter %}

{% swagger-parameter in="path" name="order" type="string" %}
Possible values: asc, desc
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://api.filswan.com" path="/miners/{{miner_id}}" method="get" summary="Single Storage Providers Detail" %}
{% swagger-description %}
This endpoint allows you to get details of the miner specified by the requested provider ID.
{% endswagger-description %}

{% swagger-response status="200" description="" %}
```
{
  "data": {
    "miner": {
      "contact_info": "Charles Cao-NBFS",
      "location": "North America",
      "max_piece_size": "32 GiB",
      "min_piece_size": "8 MiB",
      "miner_id": "f019104",
      "offline_deal_available": true,
      "price": "1.8000000000E-8",
      "score": 0,
      "status": "Active",
      "update_time_str": "1609973690",
      "verified_price": "0E-18"
    }
  },
  "status": "success"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://api.filswan.com" path="/miner/info" method="post" summary="Update Storage Provider Info" %}
{% swagger-description %}
This endpoint allows you to update your storage provider information.
{% endswagger-description %}

{% swagger-parameter in="header" name="authorization" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="miner_fid" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="bid_mode" type="integer" %}
Possible values: 1,0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="start_epoch" type="number" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="location" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="offline_deal_available" type="string" %}
Possible values: true/false 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expected_sealing_time" type="number" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

## Tasks

These endpoints return details about tasks specified by the requested IDs.

### **Public Tasks**

{% swagger baseUrl="https://api.filswan.com" path="/tasks?created_after={{created_after}}&has_miner={{has_miner}}&status={{status}}&is_public={{is_public}}&task_name={{task_name}}&type={{type}}&tags={{tags}}&max_price={{max_price}}&min_price={{min_price}}" method="get" summary="List Public Tasks" %}
{% swagger-description %}
This endpoint allows you to get a list of public tasks.
{% endswagger-description %}

{% swagger-parameter in="path" name="created_after" type="integer" %}
Filter tasks after a specific time. If empty, it shows all tasks created at any time. Value is Unix timestamp in seconds.
{% endswagger-parameter %}

{% swagger-parameter in="path" name="has_miner" type="integer" %}
Filter tasks had already been designated to a miner or not. If empty, show all tasks. Possible values: 1, 0
{% endswagger-parameter %}

{% swagger-parameter in="path" name="status" type="string" %}
Filter tasks in various status. If empty, it shows tasks in any status. Possible values: created, completed.
{% endswagger-parameter %}

{% swagger-parameter in="path" name="is_public" type="integer" %}
Tasks are public or private. Possible values: 1, 0
{% endswagger-parameter %}

{% swagger-parameter in="path" name="task_name" type="string" %}
Search tasks by task name
{% endswagger-parameter %}

{% swagger-parameter in="path" name="type" type="string" %}
The deals in this task is verified or not. Possible values: regular, verified
{% endswagger-parameter %}

{% swagger-parameter in="path" name="tags" type="string" %}
Search tasks by tags. Use comma to separate multiple tags.
{% endswagger-parameter %}

{% swagger-parameter in="path" name="max_price" type="number" %}
Max price per Gib per epoch
{% endswagger-parameter %}

{% swagger-parameter in="path" name="min_price" type="number" %}
Min price per Gib per epoch
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "data": {
    "task": [
      {
        "bid_count": 0,
        "created_on": "1614106962",
        "deal_count": 22,
        "description": "Enter up to 5 tags that best describe your task. Miner will use these tags to find task they are most interested and experienced in.\n",
        "expire_days": null,
        "is_public": 1,
        "max_price": null,
        "min_price": null,
        "miner_id": null,
        "status": "Completed",
        "successful_deal_count": 0,
        "tags": null,
        "task_file_name": "import_deal_template (3).csv",
        "task_id": 145,
        "task_name": "COMMON-CRAWL",
        "type": "regular"
      },
      {
        "bid_count": 1,
        "created_on": "1613713470",
        "deal_count": 1,
        "description": "NBFS fix auto import for API TOKEN, 8gb file, 160gb after seal",
        "expire_days": 4,
        "is_public": 1,
        "max_price": "0E-18",
        "min_price": "0E-18",
        "miner_id": null,
        "status": "Created",
        "successful_deal_count": 0,
        "tags": null,
        "task_file_name": "20210203_csv-verified-public.csv",
        "task_id": 125,
        "task_name": "NBFS fix auto import",
        "type": "verified"
      },
      {
        "bid_count": 2,
        "created_on": "1613682476",
        "deal_count": 1,
        "description": "Total of 320Gb verified deals will be 3,2Tb of power\nNeeds to be in the EU",
        "expire_days": 3,
        "is_public": 1,
        "max_price": null,
        "min_price": null,
        "miner_id": null,
        "status": "Completed",
        "successful_deal_count": 0,
        "tags": null,
        "task_file_name": "deal-empty-for-now.csv",
        "task_id": 124,
        "task_name": "10x 32Gb verified sectors - 2",
        "type": "verified"
      },
      {
        "bid_count": 0,
        "created_on": "1613682370",
        "deal_count": 1,
        "description": "Total of 320Gb verified deals will be 3,2Tb of power\nNeeds to be in the EU",
        "expire_days": 3,
        "is_public": 1,
        "max_price": null,
        "min_price": null,
        "miner_id": null,
        "status": "Completed",
        "successful_deal_count": 0,
        "tags": null,
        "task_file_name": "deal-empty-for-now.csv",
        "task_id": 123,
        "task_name": "10x 32Gb verified sectors",
        "type": "verified"
      },
      {
        "bid_count": 2,
        "created_on": "1613418605",
        "deal_count": 4,
        "description": "Designed for test miner client function, big winner will get 160gb after testing.",
        "expire_days": 2,
        "is_public": 1,
        "max_price": "1.00000000000E-7",
        "min_price": "0E-18",
        "miner_id": "f047419",
        "status": "Created",
        "successful_deal_count": 1,
        "tags": "NBFS",
        "task_file_name": "f047419-0219.csv",
        "task_id": 121,
        "task_name": "NBFS 9GB Miner client test",
        "type": "verified"
      },
      {
        "bid_count": 3,
        "created_on": "1613174281",
        "deal_count": 2,
        "description": "This deal is for testing email notifications. you will get 160gb after sealing",
        "expire_days": 4,
        "is_public": 1,
        "max_price": "1.0000000E-11",
        "min_price": "0E-18",
        "miner_id": "f03624",
        "status": "Created",
        "successful_deal_count": 0,
        "tags": null,
        "task_file_name": "f03624_20210215.csv",
        "task_id": 120,
        "task_name": "NBFS 9GB",
        "type": null
      },
      {
        "bid_count": 2,
        "created_on": "1613161109",
        "deal_count": 2,
        "description": "10x verified deal.will be 160gb after seal",
        "expire_days": 4,
        "is_public": 1,
        "max_price": "1.0000000E-11",
        "min_price": "0E-18",
        "miner_id": "f047419",
        "status": "Completed",
        "successful_deal_count": 1,
        "tags": null,
        "task_file_name": "f047419_20210212.csv",
        "task_id": 119,
        "task_name": "NBFS 9GB",
        "type": null
      },
      {
        "bid_count": 6,
        "created_on": "1612567274",
        "deal_count": 1,
        "description": "Verified deal file with 10x sealing capability ,it will be 320GB after proving\n",
        "expire_days": 3,
        "is_public": 1,
        "max_price": null,
        "min_price": null,
        "miner_id": null,
        "status": "Created",
        "successful_deal_count": 0,
        "tags": null,
        "task_file_name": "film1.csv",
        "task_id": 116,
        "task_name": "Speedium-1612567082",
        "type": "verified"
      },
      {
        "bid_count": 5,
        "created_on": "1612448401",
        "deal_count": 2,
        "description": "9Gb file with 10x sealing capability ,it will be 160GB after proving",
        "expire_days": 4,
        "is_public": 1,
        "max_price": "1.50000000000E-7",
        "min_price": "1.00000000000E-7",
        "miner_id": "f023467",
        "status": "Completed",
        "successful_deal_count": 0,
        "tags": "NA,EU",
        "task_file_name": "f023467_20210212.csv",
        "task_id": 115,
        "task_name": "Filbox Feb04-2 Task",
        "type": "verified"
      },
      {
        "bid_count": 6,
        "created_on": "1612443851",
        "deal_count": 2,
        "description": "Open to EU and NA miners",
        "expire_days": 4,
        "is_public": 1,
        "max_price": "1.5000000000E-8",
        "min_price": "1.0000000000E-8",
        "miner_id": "f010446",
        "status": "Completed",
        "successful_deal_count": 0,
        "tags": "filbox",
        "task_file_name": "f010446_20200210.csv",
        "task_id": 114,
        "task_name": "Filbox Verified deal",
        "type": "verified"
      }
    ]
  },
  "status": "success",
  "total_items": 10,
  "total_task_count": 10
}
```
{% endswagger-response %}
{% endswagger %}

### **Client Tasks**

{% swagger baseUrl="https://api.filswan.com" path="/tasks?limit={{limit}}&offset={{offset}}" method="get" summary="List User Tasks" %}
{% swagger-description %}
This endpoint allows you to get details of tasks created by a client.
{% endswagger-description %}

{% swagger-parameter in="path" name="limit" type="integer" %}
The number of items to return in the response
{% endswagger-parameter %}

{% swagger-parameter in="path" name="offset" type="integer" %}
Page number, starts from 0. Default: 0
{% endswagger-parameter %}

{% swagger-parameter in="header" name="authorization" type="string" %}
Bearer token
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "data": {
    "task": [
      {
        "bid_count": 0,
        "created_on": "1614106596",
        "deal_count": 22,
        "description": "Enter up to 5 tags that best describe your task. Miner will use these tags to find task they are most interested and experienced in.",
        "expire_days": null,
        "is_public": 0,
        "max_price": null,
        "min_price": null,
        "miner_id": "f001122",
        "status": "Completed",
        "successful_deal_count": 0,
        "tags": null,
        "task_file_name": "import_deal_template (3).csv",
        "task_id": 143,
        "task_name": "COMMON-CRAWL",
        "type": "regular"
      },
      {
        "bid_count": 0,
        "created_on": "1614106085",
        "deal_count": 39,
        "description": "It has a General Storage Service (GS2) store unstructured data such as photos, videos, log files, backups and container images compatible with Amazon S3 cloud storage service.",
        "expire_days": null,
        "is_public": 0,
        "max_price": null,
        "min_price": null,
        "miner_id": "f001122",
        "status": "Completed",
        "successful_deal_count": 0,
        "tags": null,
        "task_file_name": "import_deal_template (3).csv",
        "task_id": 142,
        "task_name": "COMMON-CRAWL",
        "type": "regular"
      }
    ]
  },
  "status": "success",
  "total_items": 2,
  "total_task_count": 2
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://api.filswan.com" path="/tasks/{{task_uuid}}?limit={{limit}}&offset={{offset}}" method="get" summary="Single Task Details" %}
{% swagger-description %}
This endpoint allows you to get details about the task specified by the requested task UUID.
{% endswagger-description %}

{% swagger-parameter in="path" name="limit" type="integer" %}
Number of items in one page. Default: 10
{% endswagger-parameter %}

{% swagger-parameter in="path" name="offset" type="integer" %}
Page number, starts from 0. Default: 0
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "data": {
    "average_bid": "0",
    "bid": [
      {
        "bid_id": 26,
        "contact_info": "slack: @Patrick - Factor8 Solutions",
        "created_on": "1613978960",
        "expire_days": 5,
        "min_piece_size": "16GB",
        "price": "0E-18",
        "proposal": "whatever you need man",
        "status": "New",
        "swan_user_info": {
          "headline": null,
          "miners": [
            {
              "location": "Global",
              "max_piece_size": "32 GiB",
              "min_piece_size": "256 B",
              "miner_id": "f03223",
              "offline_deal_available": false,
              "price": "5.000000000000000000",
              "score": 0,
              "status": "Deleted",
              "update_time_str": "1613951245947",
              "verified_price": "5.000000000000000000"
            },
            {
              "location": "Europe",
              "max_piece_size": "32 GiB",
              "min_piece_size": "16 GiB",
              "miner_id": "f062353",
              "offline_deal_available": true,
              "price": "5.0000000000E-8",
              "score": 0,
              "status": "Deleted",
              "update_time_str": "1613949072425",
              "verified_price": "0E-18"
            }
          ],
          "registered_on": "1613949072",
          "status": "Active",
          "summary": null
        },
        "task_id": 125,
        "username": "swancylmqovj",
        "won_on": null
      }
    ],
    "bid_count": 1,
    "deal": [
      {
        "created_at": "1613713470",
        "deal_cid": null,
        "file_path": null,
        "file_source_url": "https://download.nbai.io/CC-MAIN-20200918061627-20200918091627-00583-00584-00585-00586-00587-00588-00589.gz.car",
        "id": 2645,
        "md5_origin": null,
        "miner_id": null,
        "note": null,
        "start_epoch": null,
        "status": "Created",
        "task_id": 125,
        "updated_at": "1613713470",
        "user_id": 21
      }
    ],
    "deal_complete_rate": "0.00",
    "miner": null,
    "poster": {
      "complete_task_count": 39,
      "contact_info": "Charles Cao-NBFS",
      "member_since": "January 12, 2021"
    },
    "task": {
      "created_on": "1613713470",
      "description": "NBFS fix auto import for API TOKEN, 8gb file, 160gb after seal",
      "expire_days": 4,
      "is_public": 1,
      "max_price": "0E-18",
      "min_price": "0E-18",
      "miner_id": null,
      "status": "Created",
      "tags": null,
      "task_file_name": "20210203_csv-verified-public.csv",
      "task_id": 125,
      "task_name": "NBFS fix auto import",
      "type": "verified"
    },
    "total_deal_count": 1
  },
  "status": "success"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://api.filswan.com" path="/tasks" method="post" summary="Create Task" %}
{% swagger-description %}
This endpoint allows you to create a new task on FilSwan Platform.
{% endswagger-description %}

{% swagger-parameter in="header" name="authorization" type="string" %}
Bearer token
{% endswagger-parameter %}

{% swagger-parameter in="body" name="fast_retrieval" type="string" %}
Possible values: true/false
{% endswagger-parameter %}

{% swagger-parameter in="body" name="bid_mode" type="string" %}
This task is available for autobid or not. Possible values: 1, 0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="task_name" type="string" %}
Task name you prefered
{% endswagger-parameter %}

{% swagger-parameter in="body" name="is_public" type="integer" %}
This task is whether public or private. The possible values: 1, 0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" %}
The deals in this task is whether regular or verified. Possible values: regular, verified
{% endswagger-parameter %}

{% swagger-parameter in="body" name="file" type="object" %}
The CSV file containing all deal information in the task to create. It is required when creating a private task.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="miner_id" type="string" %}
The provider you want to assign the task to. Required if is_public is set to 0.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="description" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="tags" type="string" %}
Up to 5 tags. Use comma to separate multiple tags.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="max_price" type="number" %}
Max price per Gib per epoch
{% endswagger-parameter %}

{% swagger-parameter in="body" name="min_price" type="number" %}
Min price per Gib per epoch
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "data": {
    "filename": "import_deal_template.csv"
  },
  "status": "success"
}
```
{% endswagger-response %}
{% endswagger %}

### **Storage Provider Tasks**

{% swagger baseUrl="https://api.filswan.com" path="/my_miner/tasks?limit={{limit}}&offset={{offset}}" method="get" summary="List Storage Provider Tasks" %}
{% swagger-description %}
This endpoint allows you to get a list of tasks when your role is a miner.
{% endswagger-description %}

{% swagger-parameter in="path" name="limit" type="integer" %}
The number of items to return in the response. Default: 20
{% endswagger-parameter %}

{% swagger-parameter in="path" name="offser" type="integer" %}
Page number, starts from 0. Default: 0
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

### **Deals**.

{% swagger baseUrl="https://api.filswan.com" path="/offline_deals/{{miner_fid}}?deal_status={{deal_status}}&limit={{limit}}&offset={{offset}}" method="get" summary="Get storage provider's deals by status" %}
{% swagger-description %}
This endpoint allows you to get a list of offline deals belongs to a specified provider ID.
{% endswagger-description %}

{% swagger-parameter in="path" name="deal_status" type="string" %}
The deal status. Possible values: ReadyForImport, FileImporting, FileImported, DealActive, ImportFailed
{% endswagger-parameter %}

{% swagger-parameter in="path" name="limit" type="integer" %}
The number of items to return in the response. Default: 20
{% endswagger-parameter %}

{% swagger-parameter in="path" name="offset" type="integer" %}
Page number, starts from 0. Default: 0
{% endswagger-parameter %}

{% swagger-parameter in="header" name="authorization" type="string" %}
Bearer token
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "data": {
        "deal": [
            {
                "created_at": "1613398987",
                "deal_cid": "deal_cid",
                "file_path": "file_path",
                "file_source_url": "file_source_url",
                "id": 1,
                "md5_origin": null,
                "miner_id": 1,
                "note": "This is an example.",
                "start_epoch": 400300,
                "status": "ReadyForImport",
                "task_id": 1,
                "updated_at": "1613398987",
                "user_id": 1
            },
            {
                "created_at": "1613398987",
                "deal_cid": deal_cid",
                "file_path": "file_path",
                "file_source_url": "file_source_url",
                "id": 2,
                "md5_origin": null,
                "miner_id": 1,
                "note": "",
                "start_epoch": 400300,
                "status": "ReadyForImport",
                "task_id": 1,
                "updated_at": "1613398987",
                "user_id": 1
            }
        ]
    },
    "status": "success"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://api.filswan.com" path="/my_miner/deals/<deal_cid>" method="put" summary="Update Single Deal Details" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="authorization" type="string" %}
Bearer token
{% endswagger-parameter %}

{% swagger-parameter in="body" name="status" type="string" %}
The new deal status. Possible values: FileImporting, FileImported, DealActive, ImportFailed
{% endswagger-parameter %}

{% swagger-parameter in="body" name="note" type="string" %}
The additional information you would like to provide regarding the deal.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="file_path" type="string" %}
The path where the car file is downloaded.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="file_size" type="string" %}
The size of the car file.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "data": {
    "deal": {
      "created_at": "1613398987",
      "deal_cid": "deal_cid",
      "file_path": "file_path",
      "file_source_url": "file_source_url",
      "id": 1,
      "md5_origin": null,
      "miner_id": 1,
      "note": "This is a test",
      "start_epoch": 400300,
      "status": "status",
      "task_id": 1,
      "updated_at": "1613398987",
      "user_id": 18
    },
    "message": "Deal updated successfully."
  },
  "status": "Success"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://api.filswan.com" path="/my_miner/tasks/<task_uuid>/deals/<deal_cid>" method="put" summary="Update Deal Status" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="authorization" type="string" %}
Bearer token
{% endswagger-parameter %}

{% swagger-parameter in="body" name="status" type="string" %}
The new deal status. Possible values: FileImporting, FileImported, DealActive, ImportFailed
{% endswagger-parameter %}

{% swagger-parameter in="body" name="note" type="string" %}
The additional information you would like to provide regarding the deal
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "data": {
    "deal": {
      "created_at": "1613398987",
      "deal_cid": "deal_cid",
      "file_path": "file_path",
      "file_source_url": "file_source_url",
      "md5_origin": "md5_origin",
      "miner_id": 1,
      "note": "note",
      "start_epoch": 400000,
      "status": "new-status",
      "task_id": 1,
      "updated_at": "1613398987"
    },
    "message": "Status new-status updated successfully."
  },
  "status": "success"
}
```
{% endswagger-response %}
{% endswagger %}

## List of Supported API Methods

The list below documents the API methods that the FilSwan platform currently supports. When a response payload is present, all responses are returned in JSON format.

* Get Auth Token
* Generate API Key
* Generate JWT token
* List storage providers
* Single storage provider
* List Public Tasks
* List User Tasks
* Single task
* Create Task
* List storage provider Tasks
* Get storage provider's deals by status
* Update Single deal details
* Update deal status of a task



Find out more about our [APIs](https://documenter.getpostman.com/view/13140808/TWDZJbzV#intro).

If you have an API-related question, you can also discuss in the [developer community forum](https://github.com/nebulaai/swan/discussions).

