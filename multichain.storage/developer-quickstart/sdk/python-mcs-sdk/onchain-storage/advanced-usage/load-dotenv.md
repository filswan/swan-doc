---
description: How to load .env file that stores wallet informations
---

# Load Dotenv

For better security, we can load the wallet information as an environment variable (there are also other methods that can be used to store your wallet information, but using a`.env` file is recommended).&#x20;

To store your information:

```
private_key=<'private_key'>
rpc_endpoint=<'rpc_endpoint'>
api_key=<'api_key'>
access_token=<'access_token'>
```

To obtain the private key, RPC endpoint, API key and access token, check out the following guides.

#### Setup MetaMask

{% content-ref url="../../../../../mcp-user-guide/setup-metamask.md" %}
[setup-metamask.md](../../../../../mcp-user-guide/setup-metamask.md)
{% endcontent-ref %}

#### Create API Key

{% content-ref url="../../../../../../run-swan-provider/prerequisites/" %}
[prerequisites](../../../../../../run-swan-provider/prerequisites/)
{% endcontent-ref %}

To read .`env` file as environment variables. You need to import the python-dotenv package.

{% code lineNumbers="true" %}
```python
import dotenv import load_dotenv

load_dotenv(".env")
wallet_address = os.getenv('wallet_address')
private_key = os.getenv('private_key')
rpc_endpoint = os.getenv('rpc_endpoint')
```
{% endcode %}

You can also access your wallet address using the private key.

```python
from web3 import Web3

w3 = Web3(Web3.HTTPProvider(rpc_endpoint))
wallet_address = w3.eth.account.privateKeyToAccount(private_key).address
```

{% hint style="warning" %}
Be careful not to expose this information! \
Revealing your private key to others will give them access to your wallet.
{% endhint %}
