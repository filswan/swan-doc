---
description: Tutorial for accessing bucket through Python MCS SDK
---

# MCS Bucket Storage Examples

The MCS Bucket is a storage location to hold files. MCS Bucket files are referred to as objects.

This section describes how to use the python-MCS-SDK to perform common operations on the MCS bucket.

### Create an MCS Bucket

For each wallet, the name of the MCS Bucket must be unique.

```python
from mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)
# Return true if bucket created, else False
bucket_client.create_bucket(bucket_name)
```

### List existing buckets

List all the existing buckets for the MCS account

```python
from mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
for i in bucket_client.list_buckets():
    print(i.to_json())
```

### Delete existing buckets

```python
from mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)
# Return true if bucket created, else False
bucket_client.delete_bucket(bucket_name)
```

### Get specific bucket information by bucket name and bucket uid

```python
from mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)
# Return None if MCS cannot find this bucket
print(bucket_client.get_bucket("<BUCKET_NAME>","<BUCKET_UID>").to_json())
```
