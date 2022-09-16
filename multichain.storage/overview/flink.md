---
description: A data provider DAO offers Chainlink Oracle service for Filecoin Network
---

# Flink

### Introduction

Flink is a data provider DAO aiming at offering Chainlink Oracle service for the Filecoin Network. Flink offers deal information on multi chains for users who want to store their data on Filecoin.

### **What is Filecoin - Chainlink Data Provider**

Filecoin is the best option for users from blockchains like Ethereum, BSC, and Polygon to store large-scale data off-chain. Users can upload and retrieve data from the Filecoin network via sending deals. However, how to generate a cross-chain proof remains unresolved and has created a gap between users' storage needs and the Fileocin storage solution.

[An External adapter](https://docs.chain.link/docs/external-adapters) can allow access to high-quality data and enable extreme flexibility to connect smart contracts to premium web APIs. With Chainlink external adapter, user can check their deal information on oracle node operators.

{% embed url="https://github.com/filswan/flink" %}

### **Sample Use Case**

**Polygon NFTs USDC payment for Filecoin storage**

The general process of saving NFTs on the Filecoin network is:

* Lock a payment on the Polygon network
* Swap tokens to Filecoin agent
* Filecoin agents send NFT in deals to Filecoin storage providers
* Get an on-chain deal ID
* Chainlink oracle broadcasts the proof to Polygon network
* Storage DAO notaries sign the data based on the deal info provided by Chainlink oracle
* NFT payment unlocked to the Filecoin agent

![](<../../.gitbook/assets/flink image.png>)

### **Design Structure**

**Three must-haves to work as a Flink data provider:**

* Data aggregator
* Chainlink external adapter
* Data DAO notary

Several blockchain scanners will first aggregate the data to a unified data provider. Then the chainlink eternal adapter with oracle smart contracts will broadcast the proof to the targeted blockchain network. Afterward, Data notaries will sign the transaction based on the on-chain oracle data. The payment will be triggered once the on-chain proof is relayed from Chainlink oracles.

### **Data aggregator**

When a FIlecoin agent sends the data to a storage provider, the data storage process starts. The storage provider needs to accept the deal and upload an on-chain deal acceptance confirmation, which means the deal is in progress and a deal id will be generated on the Filecoin network.&#x20;

The data aggregator will scan the Filecoin deal information from different data sources and send the information as an API interface. Check the [data](https://github.com/filswan/flink/blob/main/data) directory for the scan-related code. Typical deal info is in this format:

> [http://35.168.51.2:7886/deal/5210178?network=filecoin\_mainnet](http://35.168.51.2:7886/deal/5210178?network=filecoin\_mainnet)

```
//{

    "status": "success",
    "data": {
        "deal": {
            "deal_id": 5210178,
            "deal_cid": "",
            "message_cid": "bafy2bzaceaotial6pogwzvm7woh5pf37sivrzm3fmp5teao365jl22z5q4pfc",
            "height": 1697382,
            "piece_cid": "baga6ea4seaqjffbc2mmed2piulix5qfppyuhbqumnppme5ngj3q2ol4udijjqbq",
            "verified_deal": true,
            "storage_price_per_epoch": 0,
            "signature": "",
            "signature_type": "",
            "created_at": 1649227860,
            "piece_size": "1073741824",
            "start_height": 1701360,
            "end_height": 3234661,
            "client": "f1g463yb4ok3lq3tffkvvfmfyngcagpx4kg7c7rei",
            "client_collateral_format": "000000000000000000",
            "provider": "f067375",
            "provider_tag": "",
            "verified_provider": 0,
            "provider_collateral_format": "000000000000000000",
            "status": 0,
            "network_name": "filecoin_mainnet",
            "storage_price": 0
        }
    }
}
```

### **Chainlink External Adapter - DATA DAO**

After the data aggregator gets the deal information, an External adapter is needed for offering API access for data DAO notaries in the next step.

For detailed information about how to build and deployed External Adapter, please check the code in [the adapter](https://github.com/filswan/flink/blob/main/adapter)

### **Data DAO Notary**

Data DAO notary is in charge of signing the multi-sig wallet for unlocking the fund to Filecoin agents.

The DAO contract allows the community to add or remove notaries from the DAO. The DAO notaries will follow these steps before signing:

* get deal\_id by proposal\_cid
* get deal\_id from Chainlink Filecoin adapter
  * if matches trigger DAO signature
    * match client\_address
    * match deal\_cid (proposal\_cid)
  * otherwise, waiting for the next check cycle

### **Roadmap**

* March 14th,2022: The mainnet launch with the Polygon network
* June 6th, 2022: Notary DAO setup
