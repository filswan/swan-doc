---
description: This guide will explain how to install the python-mcs-sdk and its basic usage
---

# Get Started

## Prerequisites

* [Web3](https://web3py.readthedocs.io/en/stable/) python package
* Metamask wallet - [Metamask Tutorial](../../../mcp-user-guide/setup-metamask.md)
* Polygon main net RPC - [Alchemy Tutorial](../../../mcp-user-guide/configure-metamask-with-alchemy-rpc-url.md#alchemypolygontometamaskinstructions-2.createalchemymumbaipolygonrpc) (alternatively [https://polygon-rpc.com/ ](https://polygon-rpc.com/)can be used)

#### Required python packages

* [requests](https://pypi.org/project/requests/) package - for requesting MCS APIs
* [requests-toolbelt](https://pypi.org/project/requests-toolbelt/) package - for using stream upload (to upload large files)
* [python-dotenv](https://pypi.org/project/python-dotenv/) package - for read `.env` file used to store personal informations
* [pytest](https://docs.pytest.org/en/7.1.x/) package - for testing purposes

{% hint style="info" %}
Polygon main net USDC token and MATIC are also necessary.
{% endhint %}

## Installation

**Method 1**: Install package using pip form Pypi ([https://pypi.org/project/python-mcs-sdk/](https://pypi.org/project/python-mcs-sdk/)).

<pre class="language-bash"><code class="lang-bash"><strong>pip install python-mcs-sdk</strong></code></pre>

Or **Method 2**: Install the package from GitHub ([https://github.com/filswan/python-mcs-sdk](https://github.com/filswan/python-mcs-sdk.git)).

```bash
git clone https://github.com/filswan/python-mcs-sdk.git
```

Install required packages using pip. (Method 1 will automatically install prerequisites)

```bash
pip install -r requirements.txt
```

## Environment Variables

After you have successfully setup the SDK package, your MetaMask wallet and acquired a RPC URL. Let's set some wallet informations up in an `.env` file for MCS Python SDK to access.

Note that the filename should be `.env_main` for using MCS polygon main net, and the file needs to be under the current directory for `python-dotenv` package to access.

```python
wallet_address=<'WALLET_ADDRESS'>
private_key=<'PRIVATE_KEY'>
rpc_endpoint=<'WEB3_API'>
```

{% hint style="info" %}
Be careful not to expose this information! \
Revealing your private key to others will give them access to your wallet.
{% endhint %}

## Writing SDK Scripts

To begin writing a script utilizing the SDK, create a new `.py` file. Let's create a file named `demo.py` for this guide.

At the top of this file, `import` the necessary packages for the script.

{% code lineNumbers="true" %}
```python
from mcs.api import McsAPI
from mcs.contract import ContractAPI
```
{% endcode %}

Now we can begin using the SDK.

