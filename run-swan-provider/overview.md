---
description: A specialized tool for Swan Service providers.
---

# OVERVIEW

**Swan Provider** enables hardware owners to make profits on their spare computing resources by releasing them to tenants.

The latest version of Swan Provider integrated the following resource leasing options, including:

* storage lending via Filecoin
* RPC lending via Pocket network
* more to come

The service Swan provides helps storage providers connect to the Web3 service market, making the Web3 service offering ultimately easier.

Typical Web3 markets are:

* ​[Filecoin Deal Market](https://docs.filswan.com/swan-provider/overview#filecoin-deal-market)​
* ​[Pocket Network RPC market](https://docs.filswan.com/swan-provider/overview#pocket-network)​
* [Lagrange DAO (coming soon)](broken-reference)

### **Filecoin Deal Market**

​[Filecoin](https://filecoin.io/) is making the web more secure and efficient with a decentralized data storage marketplace, protocol, and cryptocurrency.

[Filecoin Storage Market](https://spec.filecoin.io/systems/filecoin\_markets/storage\_market/) subsystem is the data entry point into the network. Storage Providers only earn power from data stored in a storage deal and all deals live on the Filecoin network. A deal is only valid when it is posted on chain with signatures from both parties and at the time of posting, there are sufficient balances for both parties locked up to honor the deal in terms of deal price and deal collateral.

Swan Provider runs on the same node as lotus miner nodes running and assists lotus miner processing deals. It makes it easy for miners to manage tasks, import deals, and synchronize deals with the Swan platform.

To better share the information with the FlilSwan client, authentication from the Swan platform is required.

![Swan Provider Business Flow](<../.gitbook/assets/image (22).png>)

![Swan Provider System Architect](<../.gitbook/assets/image (24).png>)

### Pocket Network(Coming Soon)

[Pocket](https://www.pokt.network/) provides RPC access to Ethereum, Polygon, and a dozen more blockchain networks.

### Lagrange DAO(Coming Soon)

{% embed url="https://github.com/filswan/go-swan-provider" %}
