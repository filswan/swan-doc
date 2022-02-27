---
description: A data provider DAO offers Chainlink Oracle service for Filecoin Network
---

# Flink

## Introduction

Smart contracts can pool together funds for the storage of a particular piece of data, as characterized by its unique content identifier (CID). The payment is triggered once the proof that it has been stored on the Filecoin Network is relayed from Chainlink oracles.

While a user from blockchains like Ethereum,BSC,Polygon want to store large amount of data offchain, filecoin is the best option. On Filecoin network,users can store data in and retrieve data from the Filecoin network via deals.However how to create a proof cross chain is not resolved. It is a gap between other blockchain storage needs and Fileocin storage solution.

Flink requires two components to work as a data provider:

* Data aggregator
* Chainlink external adapter
* Data DAO notary

Several blockchain scanner aggregate the data to a unified data provider, the chainlink esternal adapter with the oracle smartcontracs broadcasting the proof to target blockchain networks. Data notaries will sign the transaction based the oracle data onchain informtion.The payment is triggered once the proof that it has been stored on the Filecoin network is relayed from Chainlink oracles.

[External adapter](https://docs.chain.link/docs/external-adapters) allow access to high-quality data and enable extreme flexibility to connect smart contracts to premium web APIs. With chainlink external adapter, user can check their deal information on oracle node operator.

![](<../../.gitbook/assets/image (40).png>)

