---
description: A smart contract-based cross-chain storage gateway.
---

# Overview

### **Introduction**

Multi-Chain storage (MCS) is a smart-contract-based cross-chain storage gateway that is integrated with Oracle technology. It accelerates the mass adoption of decentralized storage by bridging multiple blockchain networks.

MCS enables users to pay for Filecoin storage with stablecoins and other Mainnet tokens while maintaining data security. Users will also obtain the payment transaction and IPFS information with Filecoin deal ID for future reference.

### High-Level Design

<figure><img src="../../.gitbook/assets/Filswan Deal Process-MCS.drawio.svg" alt=""><figcaption><p>Multi-chain Storage Design</p></figcaption></figure>

### Refundable VS Non-Refundable

_**Refundable**_ payment is the stand MCS payment model. When a user makes a payment to use storage, the fund is locked in the smart contract. The fund will be unlocked when the storage onchain proof is passed to the funding contract. Only the success storage deal will get paid, the unsuccess deal will be refunded to the user.

_**Non-Refundable**_ does not provide cross-chain validation about the online proof. The payment will be directly send to the service provider without the requirement of on-chain proof.

_**Refundable Chain**_

* Polygon
* BNB Chain

_**Non-Refundable Chain**_

* Aptos
* Sui

### **Functions**

MCS is a cutting-edge blockchain storage solution providing a data cache and presidency layer for decentralized data storage needs. With MCS, users can&#x20;

* Upload any data to the Filecoin network and IPFS.
* Pay for storage with stablecoins like USDC and other mainnet tokens.
* Mint NFTs directly to OpenSea.
* Access services by connecting a third-party wallet (MetaMask)
* Sent or get deals automatically through the build-in auto-bid system.
* Merge small files to a large CAR file.
* Support to multiple miners for storage.

### **Advantages**

Filecoin is an open-source, public cryptocurrency and digital payment system intended to be a blockchain-based cooperative digital storage and data retrieval method. As a powerful and dynamic distributed cloud storage network, Filecoin is adopted by multiple blockchain projects like Near and Polygon.

However, those individual chains or projects each operate in isolation and can hardly communicate with the others. Global users are consequently facing a large number of networks with different algorithms, transaction types, rules, etc. It prevents users from enjoying the full potential of blockchain technology.

**That is why MCS is working to guarantee the seamless interoperability of blockchains.** Since its launch, MCS has been dedicated to closing the gap by allowing users to swap other tokens to Fil to pay for data storage. MCS will bring data storage to the next level of security, decentralization, and democratization.

###

{% embed url="https://github.com/filswan/multi-chain-storage/tree/qa_single_miner" %}
