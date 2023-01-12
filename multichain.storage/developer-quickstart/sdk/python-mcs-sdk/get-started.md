---
description: Guide on how to install the python MCS SDK and its basic usage
---

# Get Started

### Required python packages

All necessary packages are within the `requirements.txt` in source code and automatically installed using PyPI.

* [requests](https://pypi.org/project/requests/) package - for requesting MCS APIs
* [requests-toolbelt](https://pypi.org/project/requests-toolbelt/) package - for using stream upload (to upload large files)
* [web3py](https://pypi.org/project/web3/) package - for communicating with Swan smart contract
* [tqdm](https://pypi.org/project/tqdm/) package - for display upload progress bar.

#### Optional python packages

* [python-dotenv](https://pypi.org/project/python-dotenv/) package - for reading `.env` file used to store personal information

## Installation

**Method 1**: Install the python-mcs-sdk package using pip from PyPI ([https://pypi.org/project/python-mcs-sdk/](https://pypi.org/project/python-mcs-sdk/)).

<pre class="language-bash"><code class="lang-bash"><strong>pip install python-mcs-sdk
</strong></code></pre>

Or **Method 2**: Build from source ([https://github.com/filswan/python-mcs-sdk](https://github.com/filswan/python-mcs-sdk.git)).

```bash
git clone https://github.com/filswan/python-mcs-sdk.git
```

Install required packages using pip. (Method 1 will automatically install prerequisites)

```bash
pip install -r requirements.txt
```

### Get API key for SDK

In order to access multichain.storage through python MCS SDK, you will need to obtain an API key and an access token. They can be obtained after logging into multichain.storage with your MetaMask wallet and use the 'Create API Key' button in the setting.

## Connect to multichian.storage

In order to use any function of python MCS SDK. We need to connect to multichain.storage using the API key and access token.

<pre class="language-python"><code class="lang-python">from dotenv import load_dotenv
from mcs import OnchainAPI, APIClient

if __name__ == "__main__":
    chain_name = 'polygon.mainnet'
    api_key = &#x3C;'api_key'>
    access_token = &#x3C;'access_token'>
    
    # connect to multichain.storage
<strong>    mcs_api = APIClient(api_key, access_token, chain_name)
</strong><strong>    
</strong><strong>    # check jwt token
</strong><strong>    print(mcs_api.token)
</strong></code></pre>

{% hint style="info" %}
Be careful not to expose this information! \
Revealing your private key to others will give them access to your wallet.
{% endhint %}
