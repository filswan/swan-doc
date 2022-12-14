---
description: Tutorial for login Buckets
---

# User Login

Buckets shares the login API with multichain.storage, you can generate a jwt token using a wallet address and the private key.

```python
api = MetaSpaceAPI(Params(chain_name).MCS_API)
jwt_token = api.get_jwt_token(info['wallet_address'], info['private_key'], "polygon.mainnet")
print(jwt_token)
```
