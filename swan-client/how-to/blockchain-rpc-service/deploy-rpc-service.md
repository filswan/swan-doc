# Deploy RPC Service

You can deploy your RPC service by the following command. And the example gives you a test case of your rpc service. More importantly, the RPC service provided by swan-client is compatible with thirteen public chain jsonrpc-api. The detail of public chain RPC-API documents and blockchain browsers can be found here

```
nohup swan-client daemon >> swan-client.log 2>&1 &
```

* Example:

```shell
$ curl --location --request POST '127.0.0.1:8099/chain/rpc' \
--header 'Content-Type: application/json' \
--data-raw '{ \
    "chain_id":"1", \
    "params": "{\"jsonrpc\":\"2.0\",\"method\":\"eth_blockNumber\",\"id\":1}"}'

output: 
       {"id":1,"jsonrpc":"2.0","result":"0xf1c622"}
```
