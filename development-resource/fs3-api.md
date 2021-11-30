# FS3 API

## Authentication

Login FilSwan Platform to get the authorization token which is used to acquire an access key pair for login FS3.

{% swagger baseUrl="https://<access_url>" path="/minio" method="get" summary="Acquire Access Key Pair" %}
{% swagger-description %}
This endpoint allows you to acquire an access key pair.
{% endswagger-description %}

{% swagger-parameter in="header" name="Bearer Token" type="string" %}
This token can be issued via Platform 'login' API.
{% endswagger-parameter %}

{% swagger-response status="200" description="The access key pair is successfully acquired." %}
```
{
    "data": {
        "access_key": "<access_key>",
        "access_url": "<access_url>",
        "secret_key": "<secret_key>"
    },
    "status": "success"
}
```
{% endswagger-response %}

{% swagger-response status="401" description="A valid authorization token is necessary to acquire the access key pair." %}
```
{
    "message": "Please provide a valid auth token.",
    "status": "fail"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/webrpc" method="post" summary="Login FS3" %}
{% swagger-description %}
This endpoint allows you to acquire a token which is designed to do authorization before performing any actions for safety consideration.
{% endswagger-description %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="string" %}
1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="jsonrpc" type="string" %}
2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
web.Login
{% endswagger-parameter %}

{% swagger-parameter in="body" name="params" type="array" %}
Input 'username' which is 'access_key', and 'password' which is 'secret_key'.
{% endswagger-parameter %}

{% swagger-response status="200" description="Successfully login." %}
```
{"jsonrpc":"2.0","result":{"token":"<bearer_token>","uiVersion":"2019-09-11T18:31:07Z"},"id":1}
```
{% endswagger-response %}
{% endswagger %}

## Bucket Management

{% swagger baseUrl="https://<access_url>" path="/minio/webrpc" method="post" summary="Get Bucket List" %}
{% swagger-description %}
This endpoint allows you to get a list of all buckets.
{% endswagger-description %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="string" %}
1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="jsonrpc" type="string" %}
2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
web.ListBuckets
{% endswagger-parameter %}

{% swagger-parameter in="body" name="params" type="array" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="Successfully got bucket list." %}
```
{"jsonrpc":"2.0","result":{"buckets":[{"name":"<example1>","creationDate":"2021-06-07T01:19:38.758964923Z"},{"name":"<example2>","creationDate":"2021-07-08T23:55:02.836502071Z"}],"uiVersion":"2019-09-11T18:31:07Z"},"id":1}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/webrpc" method="post" summary="Create Bucket" %}
{% swagger-description %}
This endpoint allows you to create a bucket.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="string" %}
1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="jsonrpc" type="string" %}
2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
web.MakeBucket
{% endswagger-parameter %}

{% swagger-parameter in="body" name="params" type="array" %}
input 'bucketName'
{% endswagger-parameter %}

{% swagger-response status="200" description="Successfully created the bucket." %}
```
{"jsonrpc":"2.0","result":{"uiVersion":"2019-09-11T18:31:07Z"},"id":1}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/webrpc" method="post" summary="Delete Bucket" %}
{% swagger-description %}
This endpoint allows you to delete the bucket you selected.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="string" %}
1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="jsonrpc" type="string" %}
2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
web.DeleteBucket
{% endswagger-parameter %}

{% swagger-parameter in="body" name="params" type="array" %}
Input 'bucketName'
{% endswagger-parameter %}

{% swagger-response status="200" description="Successfully deleted the bucket." %}
```
{"jsonrpc":"2.0","result":{"uiVersion":"2019-09-11T18:31:07Z"},"id":1}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/webrpc" method="post" summary="Get Bucket Policy List" %}
{% swagger-description %}
This endpoint allows you to get a list of policies of the bucket you selected.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="string" %}
1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="jsonrpc" type="string" %}
2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
web.ListAllBucketPolicies
{% endswagger-parameter %}

{% swagger-parameter in="body" name="params" type="array" %}
Input 'bucketName'
{% endswagger-parameter %}

{% swagger-response status="200" description="Successfully got the policy list." %}
```
{"jsonrpc":"2.0","result":{"uiVersion":"2019-09-11T18:31:07Z","policies":[{"bucket":"<bucket_name>","prefix":"<policy_name>","policy":"<policy_type>"}]},"id":1}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/webrpc" method="post" summary="Edit Bucket Policy" %}
{% swagger-description %}
This endpoint allows you to add or remove a policy of the bucket you selected.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' Api.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="string" %}
1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="jsonrpc" type="string" %}
2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
web.SetBucketPolicy
{% endswagger-parameter %}

{% swagger-parameter in="body" name="params" type="array" %}
Input 'bucketName', 'policy', 'prefix'
{% endswagger-parameter %}

{% swagger-response status="200" description="Successfully edited bucket policy." %}
```
{"jsonrpc":"2.0","result":{"uiVersion":"2019-09-11T18:31:07Z"},"id":1}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/deals/<bucket>" method="post" summary="Backup Bucket to Filecoin - online deal" %}
{% swagger-description %}
This endpoint allows you to backup the bucket you selected to Filecoin network as an online deal.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="MinerId" type="string" %}
provider ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Price" type="string" %}
unit: fil
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Duration" type="string" %}
unit: epoch
{% endswagger-parameter %}

{% swagger-parameter in="body" name="VerifiedDeal" type="string" %}
true/false
{% endswagger-parameter %}

{% swagger-parameter in="body" name="FastRetrieval" type="string" %}
true/false
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "data": {
        "filename": "~/minio-data/test_deals.zip",
        "walletAddress": "h376xbytsd3jie6ermpw",
        "verifiedDeal": "false",
        "fastRetrieval": "true",
        "dataCid": "bafk2bza5dgw6pubjodkscqpg",
        "minerId": "t03354",
        "price": "0.000005",
        "duration": "518800",
        "dealCid": "bafyreicvqh7krdhdnpkqwokze",
        "timeStamp": "1629835134146540"
    },
    "status": "success",
    "message": "success"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/offlinedeals/<bucket>" method="post" summary="Backup Bucket to Filecoin - offline deal" %}
{% swagger-description %}
This endpoint allows you to backup the bucket you selected to Filecoin network as an offline deal.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="Task_Name" type="string" %}
Task name you preferred.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Curated_Dataset" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="Description" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="Is_Public" type="string" %}
The task is whether public or private. The possible values: 1, 0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Type" type="string" %}
The deals in this task is whether regular or verified. the possible values: regular, verified.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Miner_Id" type="string" %}
The provider you want to assign the task to. Required if is_public is set to 0.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Min_Price" type="string" %}
Min price per Gib per epoch.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Max_Price" type="string" %}
Max price per Gib per epoch.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Tags" type="string" %}
Up to 5 tags.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Expire_Days" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="Auto_bid" type="string" %}
The task is available to auto-bid or not. The possible values: 1, 0. Required if is_public is set to 1.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "data": {
        "bucket_name": "test",
        "deals": {
            "data": {
                "taskname": "test-name",
                "filename": "be450523-52ed-44f9-9828-8e382c0d15c8.csv",
                "uuid": "d2d79d42-6f79-46fe-97bd-cd6f69c25116"
            },
            "status": "success",
            "message": "Task created successfully.A notification email has been sent to the storage provider"
        }
    },
    "status": "success",
    "message": "success"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/bucket/retrieve/<bucket>" method="get" summary="Retrieve Bucket from Filecoin - online deal" %}
{% swagger-description %}
This endpoint allows you to retrieve the bucket you selected from Filecoin network.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "data": {
        "bucket_name": "20210824",
        "deals": [
            {
                "data": {
                    "filename": "~/minio-data/test_deals.zip",
                    "walletAddress": "t3u7pum2vzyasg7cimkpnojqd3jie6erm",
                    "verifiedDeal": "false",
                    "fastRetrieval": "true",
                    "dataCid": "bafykbvgxdpej7neeoqsnvuzppme",
                    "minerId": "t03354",
                    "price": "0.000005",
                    "duration": "518700",
                    "dealCid": "bafyrekm3lmusljgmvyriqid6kcaoed5kni",
                    "timeStamp": "1629816006709676"
                },
                "status": "success",
                "message": "success"
            },
            {
                "data": {
                    "filename": "~/minio-data/test_deals.zip",
                    "walletAddress": "t3u7khtadjzfydxxdanojqd3jie6ermpw",
                    "verifiedDeal": "false",
                    "fastRetrieval": "true",
                    "dataCid": "bafykbnvz5rgs7obwbfztqrr4ahwjue",
                    "minerId": "t03354",
                    "price": "0.000005",
                    "duration": "518800",
                    "dealCid": "bafyrgigdm4ppqzwt4vufm4m3pmuvolnfe",
                    "timeStamp": "1629833844752891"
                },
                "status": "success",
                "message": "success"
            }
        ]
    },
    "status": "success",
    "message": "success"
}
```
{% endswagger-response %}
{% endswagger %}

## Object Management

{% swagger baseUrl="https://<access_url>" path="/minio/webrpc" method="post" summary="Get Objects List" %}
{% swagger-description %}
This endpoint allows you to get a list of all objects of the bucket you selected. 
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="string" %}
1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="jsonrpc" type="string" %}
2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
web.ListObjects
{% endswagger-parameter %}

{% swagger-parameter in="body" name="params" type="array" %}
Input 'bucketName', 'prefix'
{% endswagger-parameter %}

{% swagger-response status="200" description="Successfully get objects List" %}
```
{"jsonrpc":"2.0","result":{"objects":[{"name":"example_file","lastModified":"2021-06-07T01:19:38.758964923Z","size":0,"contentType":"application/octet-stream"}],"writable":true,"uiVersion":"2019-09-11T18:31:07Z"},"id":1}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/upload/<bucket>/<object>" method="put" summary="Upload Object" %}
{% swagger-description %}
This endpoint allows you to upload objects to the bucket you selected.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-amz-date" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="object" type="object" %}
Select the file you desired to upload.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/webrpc" method="post" summary="Get URL Token" %}
{% swagger-description %}
This endpoint allows you to get a URL token for downloading objects.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="string" %}
1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="jsonrpc" type="string" %}
2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
web.CreateURLToken
{% endswagger-parameter %}

{% swagger-parameter in="body" name="params" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="Successfully downloaded the object." %}
```
{"jsonrpc":"2.0","result":{"token":"<bearer_token>","uiVersion":"2019-09-11T18:31:07Z"},"id":1}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/download/<bucket>/<object>" method="get" summary="Download Objects" %}
{% swagger-description %}
This endpoint allows you to download objects.
{% endswagger-description %}

{% swagger-parameter in="path" name="token" type="string" %}
This token is issued via 'get URL Token' API.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/webrpc" method="post" summary="Delete Object" %}
{% swagger-description %}
This endpoint allows you to delete the object you selected.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API
{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="header" name="x-amz-date" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="string" %}
1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="jsonrpc" type="string" %}
2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
web.RemoveObject
{% endswagger-parameter %}

{% swagger-parameter in="body" name="params" type="array" %}
Input 'bucketName', 'objects'
{% endswagger-parameter %}

{% swagger-response status="200" description="Successfully deleted the object." %}
```
{"jsonrpc":"2.0","result":{"uiVersion":"2019-09-11T18:31:07Z"},"id":1}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/webrpc" method="post" summary="Share Object" %}
{% swagger-description %}
This endpoint allows you to share the object you selected.
{% endswagger-description %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="string" %}
1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="jsonrpc" type="string" %}
2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
web.PresignedGet
{% endswagger-parameter %}

{% swagger-parameter in="body" name="params" type="array" %}
Input 'bucket', 'expiry', 'host', 'object'.
{% endswagger-parameter %}

{% swagger-response status="200" description="Successfully get the sharable link." %}
```
{"jsonrpc":"2.0","result":{"uiVersion":"2019-09-11T18:31:07Z","url":"<object_directory>?X-Amz-Algorithm=AWS4-HMAC-SHA256\u0026X-Amz-Credential=UBFSNUG8AZIII4XOMUTW%2F20210903%2F%2Fs3%2Faws4_request\u0026X-Amz-Date=20210903T182225Z\u0026X-Amz-Expires=<expiry_time>\u0026X-Amz-SignedHeaders=host\u0026X-Amz-Signature=d35eb873a0c3bb0ea316c550b6259ce5f5eb7ba08da8a5c813721eae1f654b78"},"id":1}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/deal/<bucket>/<object>" method="post" summary="Backup Object to Filecoin - online deal" %}
{% swagger-description %}
This endpoint allows you to backup the object you selected to Filecoin network.
{% endswagger-description %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="MinerId" type="string" %}
provider ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Price" type="string" %}
unit: fil
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Duration" type="string" %}
unict: epochs
{% endswagger-parameter %}

{% swagger-parameter in="body" name="VerifiedDeal" type="string" %}
true/false
{% endswagger-parameter %}

{% swagger-parameter in="body" name="FastRetrival" type="string" %}
true/false
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "data": {
        "filename": "~/minio-data/test/waymo.zip",
        "walletAddress": "wabkhtadjzfydxxda2vzyasg7cimd3jie6ermpw",
        "verifiedDeal": "false",
        "fastRetrieval": "true",
        "dataCid": "bafykbzaceb5cfdrbg45khvhk4mza6",
        "minerId": "t03354",
        "price": "0.000005",
        "duration": "1036700",                    //epochs
        "dealCid": "bafyreicmqtttadqdksrqvunxhcgvfvb47m",
        "timeStamp": "1628025191856290"           //miliseconds
    },
    "status": "success",
    "message": "success"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/retrieve/<bucket>/<object>" method="get" summary="Retrieve Object from Filecoin - online deal" %}
{% swagger-description %}
This endpoint allows you to retrieve the object you selected from Filecoin network.
{% endswagger-description %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "data": {
        "file_name": "waymo.zip",
        "deals": [
            {
                "data": {
                    "filename": "~/minio-data/test/waymo.zip",
                    "walletAddress": "5wabkhtadjzfydxxdq66j4dubbhwpnojqd3jmpw",
                    "verifiedDeal": "false",
                    "fastRetrieval": "true",
                    "dataCid": "bafykbzaceb5cfdpdupjd4mza6",
                    "minerId": "t03354",
                    "price": "0.000005",
                    "duration": "1036700",
                    "dealCid": "bafyreicmm2g654",
                    "timeStamp": "1628025191856290"
                },
                "status": "success",
                "message": "success"
            },
            {
                "data": {
                    "filename": "~/minio-data/testre/waymo.zip",
                    "walletAddress": "5wabkhtadjzfydxxda2vzyasg7cimkcphswrq66j4dubbhwpnoj",
                    "verifiedDeal": "false",
                    "fastRetrieval": "true",
                    "dataCid": "bafykbzaceb5cfdpdupjd4mza6",
                    "minerId": "t03354",
                    "price": "0.000005",
                    "duration": "1036700",
                    "dealCid": "bafyreijg227wlo4bge76bcxk7cw",
                    "timeStamp": "1628026238100552"
                },
                "status": "success",
                "message": "success"
            }
        ]
    },
    "status": "success",
    "message": "success"
}
```
{% endswagger-response %}
{% endswagger %}

## General Settings

{% swagger baseUrl="https://<access_url>" path="/minio/webrpc" method="post" summary="Change Password" %}
{% swagger-description %}
This endpoint allows you to change password.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="string" %}
1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="jsonrpc" type="string" %}
2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
web.SetAuth
{% endswagger-parameter %}

{% swagger-parameter in="body" name="params" type="array" %}
Input 'currentAccessKey', 'currentSecretKey', 'newAccessKey', 'newSecretKey'.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/webrpc" method="post" summary="Get Storage Info" %}
{% swagger-description %}
This endpoint allows you to get storage information.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
The bearer token is issued via 'login FS3' API.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="string" %}
1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="jsonrpc" type="string" %}
2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
web.StorageInfo
{% endswagger-parameter %}

{% swagger-parameter in="body" name="params" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="Successfully got storage info." %}
```
{"jsonrpc":"2.0","result":{"storageInfo":{"Used":653465,"Total":7537270108160,"Available":4140889018368,"Backend":{"Type":1,"OnlineDisks":0,"OfflineDisks":0,"StandardSCData":0,"StandardSCParity":0,"RRSCData":0,"RRSCParity":0,"Sets":null}},"uiVersion":"2019-09-11T18:31:07Z"},"id":1}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://<access_url>" path="/minio/webrpc" method="post" summary="Get Server Info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="header" name="User-Agent" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" type="string" %}
1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="jsonrpc" type="string" %}
2.0
{% endswagger-parameter %}

{% swagger-parameter in="body" name="method" type="string" %}
web.ServerInfo
{% endswagger-parameter %}

{% swagger-parameter in="body" name="params" type="string" %}

{% endswagger-parameter %}

{% swagger-response status="200" description="Successfully got server info." %}
```
{"jsonrpc":"2.0","result":{"MinioVersion":"2019-09-11T18:33:15Z","MinioMemory":"Used: 6.8 MB | Allocated: 3.7 GB | Used-Heap: 6.8 MB | Allocated-Heap: 65 MB","MinioPlatform":"Host: 2f245ecded89 | OS: linux | Arch: amd64","MinioRuntime":"Version: go1.13 | CPUs: 24","MinioGlobalInfo":{"isBrowserEnabled":true,"isDistXL":false,"isEnvBrowser":false,"isEnvCreds":false,"isEnvRegion":false,"isSSL":false,"isWorm":false,"isXL":false,"serverRegion":""},"MinioUserInfo":{"isIAMUser":false},"uiVersion":"2019-09-11T18:31:07Z"},"id":1}
```
{% endswagger-response %}
{% endswagger %}
