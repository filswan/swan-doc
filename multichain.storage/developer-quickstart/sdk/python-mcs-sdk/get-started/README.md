---
description: This guide will explain how to install the python-mcs-sdk and its basic usage
---

# Get Started

### Required python packages

All necessary packages are within the `requirements.txt` in source code and automatically installed using pypi.

* [requests](https://pypi.org/project/requests/) package - for requesting MCS APIs
* [requests-toolbelt](https://pypi.org/project/requests-toolbelt/) package - for using stream upload (to upload large files)
* [web3py](https://pypi.org/project/web3/) package - for communicate with Swan smart contract

#### Optional python packages

* [python-dotenv](https://pypi.org/project/python-dotenv/) package - for read `.env` file used to store personal informations
* [pytest](https://docs.pytest.org/en/7.1.x/) package - for testing purposes

## Installation

**Method 1**: Install package using pip form pypi ([https://pypi.org/project/python-mcs-sdk/](https://pypi.org/project/python-mcs-sdk/)).

<pre class="language-bash"><code class="lang-bash"><strong>pip install python-mcs-sdk</strong></code></pre>

Or **Method 2**: Build from source ([https://github.com/filswan/python-mcs-sdk](https://github.com/filswan/python-mcs-sdk.git)).

```bash
git clone https://github.com/filswan/python-mcs-sdk.git
```

Install required packages using pip. (Method 1 will automatically install prerequisites)

```bash
pip install -r requirements.txt
```

## Environment Variables

After you have successfully setup the SDK package, your MetaMask wallet and acquired a RPC URL. Let's set some wallet informations up in an `.env` file for MCS Python SDK to access.

We recommend to store wallet information use `env` for security messaure. There are also other methods can be used.

```python
wallet_address=<'WALLET_ADDRESS'>
private_key=<'PRIVATE_KEY'>
rpc_endpoint=<'WEB3_API'>
```

{% hint style="info" %}
Be careful not to expose this information! \
Revealing your private key to others will give them access to your wallet.
{% endhint %}



