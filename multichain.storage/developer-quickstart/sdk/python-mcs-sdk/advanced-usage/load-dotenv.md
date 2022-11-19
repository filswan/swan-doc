---
description: How to load .env file that stores wallet informations
---

# Load Dotenv

Before start working with SDK, we need to load the wallet informations as environment variable (there are also other methods that can be used to store your wallet informations, but `.env` file is recommended). To read .`env` file as environment variables. You needs to import the python-dotenv package.

{% code lineNumbers="true" %}
```python
import dotenv import load_dotenv

load_dotenv(".env_main")
wallet_address = os.getenv('wallet_address')
private_key = os.getenv('private_key')
rpc_endpoint = os.getenv('rpc_endpoint')
```
{% endcode %}

You can also access your wallet address use private key.

```python
from web3 import Web3

w3 = Web3(Web3.HTTPProvider(rpc_endpoint))
walletAddress = w3.eth.account.privateKeyToAccount(private_key).address
```

