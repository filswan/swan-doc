---
description: A specialized tool for Swan Service providers.
---

# Overview

## Introduction

&#x20;Web3 service providers provide service for different blockchains included but not limit to Filecoin, AR, Polygon RPC service. With FilSwan service provide, we connected to web3 service market to make the web3 service offering ultimated easier.

Typical Web3 markets are:

* [Filecoin Deal Market](overview.md#filecoin-deal-market)
* [Pocket Network RPC market](overview.md#pocket-network)
* Ocean Protocol Data market

#### **Filecoin Deal Market**

__[_Filecoin_](https://filecoin.io/) is making the web more secure and efficient with a decentralized data storage marketplace, protocol, and cryptocurrency.

[Filecoin **** Storage Market ](https://spec.filecoin.io/systems/filecoin\_markets/storage\_market/)subsystem is the data entry point into the network. Storage miners only earn power from data stored in a storage deal and all deals live on the Filecoin network. A deal is only valid when it is posted on chain with signatures from both parties and at the time of posting, there are sufficient balances for both parties locked up to honor the deal in terms of deal price and deal collateral.

Swan Provider runs on the same node as lotus miner nodes running and assistant lotus miner process deals. It makes it easy for miners to manage tasks, import deals, and synchronize deals with the Swan platform.

In order better share the information with the Flilswan client, authentication from the Filswan platform is required.

![Swan Provider Business Flow](<../.gitbook/assets/image (22).png>)

![Swan Provider System Architect](<../.gitbook/assets/image (24).png>)

#### Pocket Network(Coming Soon)

__[_Pocket_](https://www.pokt.network/) provides RPC access to Ethereum, Polygon, and a dozen more blockchain _networks_. Everything from testnets to mainnets to any open-source interface.

{% embed url="https://github.com/filswan/go-swan-provider" %}
