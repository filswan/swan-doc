---
description: This guide will explain how to install the python-mcs-sdk and its basic usage
---

# Get Started

## Prerequisites

* [Web3](https://web3py.readthedocs.io/en/stable/) python package
* Polygon Mumbai Testnet Wallet - [Metamask Tutorial](../../../mcp-user-guide/setup-metamask.md)
* Polygon Mumbai Testnet Alchemy RPC - [Alchemy Tutorial](../../../mcp-user-guide/configure-metamask-with-alchemy-rpc-url.md#alchemypolygontometamaskinstructions-2.createalchemymumbaipolygonrpc)
* [pytest](https://docs.pytest.org/en/7.1.x/) package (for testing purposes)

Mumbai Testnet USDC and MATIC funds are also necessary - [Swan Faucet Tutorial](../../../../development-resource/swan-token-contract/acquire-testnet-usdc-and-matic-tokens.md)

## Installation

Install package using pip

```
pip install python-mcs-sdk
```

Or Install the package from [https://github.com/filswan/python-mcs-sdk](https://github.com/filswan/python-mcs-sdk.git).

```
$ git clone https://github.com/filswan/python-mcs-sdk.git
```

Install required packages using pip.

```
pip install -r requirements.txt
```

## Environment Variables

Once you have your Mumbai wallet and RPC URL, store your wallet's private key and the RPC URL.

```
wallet_info = {
  'wallet_address' : <'WALLET_ADDRESS'>
  'private_key' : <'PRIVATE_KEY'>
  'web3_api' : '<'WEB3_API'>
}
```

{% hint style="info" %}
Be careful not to expose this information! \
Revealing your private key to others will give them access to your wallet.
{% endhint %}

## Writing SDK Scripts

To begin writing a script utilizing the SDK, create a new `.py` file. Let's create a file named `demo.py`

At the top of this file, require the necessary packages for the script. (pytest is only necessary if you are running a test)

```
from mcs.api import McsAPI
from mcs.contract import ContractAPI
```

Next, after requiring the SDK, set up the wallet information.

```
wallet_info = {
        'wallet_address' : '*',
        'private_key' : '*',
        'web3_api' : '*',
    }
```

Now we can begin using the SDK methods.

