# RPC Command Service

The RPC command can help you query the latest chain height and wallet balance, the cases of Ethereum and Binance Smart Chain are as follows:

## Ethereum Mainnet:

```
# query the current height
$ swan-client rpc height --chain ETH

output:
        Chain: ETH
        Height: 15844685

# query the balance of the current height wallet
$ swan-client rpc balance --chain ETH --address 0x29D5527CaA78f1946a409FA6aCaf14A0a4A0274b
    
output:
        Chain: ETH
        Height: 15844698
        Address: 0x29D5527CaA78f1946a409FA6aCaf14A0a4A0274b
        Balance: 749.53106079798394945
```

## Binance Smart Chain Mainnet:

```
# query the current height
$ swan-client rpc height --chain BNB

output:
        Chain: BNB
        Height: 22558967

# query the balance of the current height wallet
$ swan-client rpc balance --chain BNB --address 0x4430b3230294D12c6AB2aAC5C2cd68E80B16b581

output:
        Chain: BNB
        Height: 22559008
        Address: 0x4430b3230294D12c6AB2aAC5C2cd68E80B16b581
        Balance: 0.027942338705784518
```

* More examples can be seen [here](https://github.com/filswan/go-swan-client/blob/main/document/rpc-cmd-example.md).
