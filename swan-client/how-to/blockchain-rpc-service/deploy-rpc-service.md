# Deploy RPC Service

You can deploy your RPC service by the following command. And the example gives you a test case of your RPC service. More importantly, the RPC service provided by swan-client is compatible with thirteen public chain jsonrpc-api.

You can find more public chain RPC-API documentation and blockchain browsers [here](https://github.com/filswan/go-swan-client/blob/main/document/rpc-cmd-example.md).

```
nohup swan-client daemon >> swan-client.log 2>&1 &
```

* Example `eth_blockNumber` :

```
curl --location --request POST '127.0.0.1:8099/chain/rpc' \
--header 'Content-Type: application/json' \
--data-raw '{
    "chain_id": "1",
    "params": "{\"jsonrpc\":\"2.0\",\"method\":\"eth_blockNumber\",\"id\":1}"
}'
```

* Example `eth_signTransaction` :

```
curl --location --request POST '127.0.0.1:8099/chain/rpc' \
--header 'Content-Type: application/json' \
--data-raw '{
    "chain_id": "1",
    "params": "{\"jsonrpc\":\"2.0\",\"method\":\"eth_signTransaction\",\"params\": [{\"data\":\"0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675\",\"from\": \"0xb60e8dd61c5d32be8058bb8eb970870f07233155\",\"gas\": \"0x76c0\",\"gasPrice\": \"0x9184e72a000\",\"to\": \"0xd46e8dd67c5d32be8058bb8eb970870f07244567\",\"value\": \"0x9184e72a\"}], \"id\":1}"
}'
```
