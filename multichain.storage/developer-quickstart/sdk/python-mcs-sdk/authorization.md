---
description: How to complete verification to access pirvate MCS APIs
---

# Authentication

To access most MCS APIs, you will need to complete authorization with jwt toke.\
The function `MCS.get_jwt_token` allows authorization using signature generate with `wallet_address` and `private_key`.

By initialize a new `MCS` instance and calling the `get_jwt_token(wallet_address, private_key, chain_name)`, the token will store within the current `MCS` instance for the use in the current session. (Currently there is only one chain on MCS which is "polygon\_mainnet")

example:

<pre class="language-python" data-line-numbers><code class="lang-python"><strong>api = McsAPI(Params().MCS_API)
</strong>jwt_token = api.get_jwt_token(wallet_address, private_key, "polygon.mainnet")
print(api.jwt_token)</code></pre>

The token will be used for accessing most of the MCS APIs that are not public.&#x20;

{% hint style="info" %}
Token will expire after 10 hours.
{% endhint %}

