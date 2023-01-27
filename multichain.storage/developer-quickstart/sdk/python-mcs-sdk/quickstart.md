---
description: Guide on how to install the python MCS SDK and its basic usage
---

# Quickstart

This guide details the steps required to install or update the python MCS SDK.

### Installation

To use python-MCS-SDK, you first need to install it and its dependencies.

#### Install or update Python

Before installing python-MCS-SDK, install Python 3.7 or later; support for Python 3.6 and earlier is deprecated. After the deprecation date listed for each Python version, new releases of python-MCS-SDK will not include support for that version of Python.

For information about how to get the latest version of Python, see the official [Python documentation](https://www.python.org/downloads/).

## Install python-MCS-SDK

Install the latest python-MCS-SDK release via **pip:**

`pip install python-MCS-SDK`

{% hint style="info" %}
The latest development version of python-MCS-SDK is on [GitHub](https://github.com/filswan/python-mcs-sdk)
{% endhint %}

### Configuration

Before using python-MCS-SDK, you need to generate an API key through the [MCS website](https://www.multichain.storage/#/my\_account) for login. Make sure to save your API key and Access Token after you have caused it. You will not find it again after you create it.

Also, to use python-mcs-sdk's Onchain upload feature, you need to provide an RPC endpoint. Polygon mainnet MATIC and USDC Token are also required to make payments.

### Using python-MCS-SDK

To use python-MCS-SDK, you must first import it and state your identity.

```python
from mcs import APIClient
# Let's initialize the Python-MCS-SDK
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
# polygon.mainnet for mainnet, polygon.mumbai for testnet
```

If you see "Login Successful" in the console, you have logged in successfully. Now you can choose which service you want to initialize, either Onchain or Buckets. The following code will take you through the initialization of both services.

```python
from mcs import BucketAPI, OnchainAPI
# Init bucket client
bucket_client = BucketAPI(mcs_api)
# Init onchain client
onchain_client = OnchainAPI(mcs_api)
```
