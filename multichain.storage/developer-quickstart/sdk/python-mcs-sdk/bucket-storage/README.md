---
description: Tutorial for accessing meta space through Python MCS SDK
---

# Bucket Storage

### Introduction

Bucket allows users to create buckets for file storage and backup.

### Connect to Bucket

Connect to Bucket by login into MCS first.

```python
from mcs import APIClient, BucketAPI

mcs_api = APIClient(<'api_key'>, <'access_token'>, 'polygon.mainnet')
bucket_api = BucketAPI(mcs_api)
```
