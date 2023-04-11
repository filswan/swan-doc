---
description: Advanced method to use python MCS SDK
---

# Advanced Usage

### Introduction

This guide allows users to customize their usage of python MCS SDK.

### Connect to Onchain Storage

First, connect to onchain storage with MCS API key login.

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient(<'api_key'>, <'access_token'>, 'polygon.mainnet')
onchain_api = Onchain(mcs_api)
```
