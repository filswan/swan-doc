# Developer Quickstart

Multi-Chain Payment (hereinafter called the 'MCP') is a suite of Ethereum scaling solutions that enables high-throughput, low cost smart contracts while remaining trustworthy secure.&#x20;

The following documentation describes how to use MCP, which is currently live on Polygon Mumbai Testnet. Whether you're a developer that just wants to start building or you're curious into digging deeper into the internals of MCP and how it works, this site is the right place for you.

### System Design

![](<../.gitbook/assets/image (29) (1).png>)

### How does MCP work? <a href="#how-does-arbitrum-work" id="how-does-arbitrum-work"></a>

If you're looking to discover how MCP works, the best place to begin is by the [User Guide](mcp-user-guide.md) section, which gives a high level overview of MCP's internals. From there, you can jump into more detailed explainers on various components of the system.

### How Can I Start Building <a href="#how-can-i-start-building" id="how-can-i-start-building"></a>

#### Modules <a href="#__docusaurus" id="__docusaurus"></a>

* **\[Token Swap]\(#Token Swap):** Token Swap module is in charge of swap the user's token to wrapped token, it can be USDC or other tokens.
* **Lock payment:** When a user upload a file, the lock fee that the user needs to pay will be calculated based on the average provider price.
* **DAO Signature:** If Dao detects that the file uploaded by the user has been on chain, it will trigger a signature operation.
* **Unlock payment:** When a specific number of DAO have signed, the unlock operation will be triggered. The part that needs to be paid will be deducted from the locked token, and the remaining token will be returned to the user.
* **Data DAO:** More information can be find at [Flink](https://github.com/filswan/flink).
* **IPFS/Filecoin Storage**

#### Getting Started with PaymentBridge:

1 Clone code to $GOPATH/src

```
git clone https://github.com/filswan/multi-chain-payment
```

2 Pull-in the submodules:

```
cd $GOPATH/src/payment-bridge/
git submodule update --init --recursive
make ffi
```

3 Build project

After enter 'payment-bridge' directory, and execute the make command, you can get a runnable binary file named payment\_bridge and config file in $GOPATH/src/payment-bridge/config/.

```
cd $GOPATH/src/payment-bridge/
GO111MODULE=on make
```

4 Run the project

Enter 'payment-bridge/build' directory, and execute the binary file of the payment-bridge project.\
Before start running the payment bridge project, you need to read the section about config introduction below and fill in the configuration items as required.

```
cd $GOPATH/src/payment-bridge/build/`
chmod +x payment-bridge
./payment_bridge
```

{% hint style="info" %}
**Note:** Taking payment on the polygon network as an example, before running the ./payment-bridge command, you need to edit two config file:

* $GOPATH/src/payment-bridge/build/config/config.toml
* $GOPATH/src/payment-bridge/build/config/polygon/config\_polygon.toml
{% endhint %}

#### Configuration

You need to modify the config file and input your config params, the configuration items will be introduced below:

#### config.toml

* **admin\_wallet\_on\_polygon:** The wallet address used to execute contract methods on the polygon network and pay for gas
* **swan\_payment\_address\_on\_polygon:** The contract address of the swan payment gateway, used for lock and unlock user fees on polygon
* **file\_coin\_wallet:** The wallet address of the user's paying for storage file to the filecoin network

**\[lotus]**

* **api\_url:** Url of lotus client web api, such as: **http://\[ip]:\[port]/rpc/v0**, generally the \[port] is **1234**. See [Lotus API](https://docs.filecoin.io/reference/lotus-api/)
* **access\_token:** Access token of lotus market web api. When market and miner are not separate, it is also the access token of miner access token. See [Obtaining Tokens](https://docs.filecoin.io/build/lotus/api-tokens/#obtaining-tokens)

**\[ipfs\_server]**

ipfs-server is used to upload and download generated Car files. You can upload generated Car files via `upstream_url` and storage provider will download Car files from this ipfs-server using `download_stream_url`. The downloadable URL in the CSV file is built with the following format: host+port+ipfs+hash, e.g. [http://host](http://host): port/ipfs/QmPrQPfGCAHwYXDZDdmLXieoxZP5JtwQuZMUEGuspKFZKQ

**\[swan\_task]**

* **dir\_deal:** Output directory for saving generated Car files and CSVs
* **verified\_deal:** \[true/false] Whether deals in this task are going to be sent as verified
* **fast\_retrieval:** \[true/false] Indicates that data should be available for fast retrieval
* **start\_epoch\_hours:** start\_epoch for deals in hours from current time
* **expired\_days:** expected completion days for storage provider sealing data
* **max\_price:** Max price willing to pay per GiB/epoch for offline deal
* **min\_price:** Min price willing to pay per GiB/epoch for offline deal
* **generate\_md5:** \[true/false] Whether to generate md5 for each car file, note: this is a resource consuming action
* **relative\_epoch\_from\_main\_network:** The difference between the block height of filecoin's mainnet and testnet. If the filecoin testnet is linked, this configuration item is set to -858481, and if the link is the mainnet, it is set to 0

#### config\_polygon.toml

Currently, USDC is supported for payment. Take polygon network as an example to introduce configuration items

**\[polygon\_mainnet\_node]**

* **rpc\_url:** the polygon network rpc url
* **payment\_contract\_address:** swan payment gateway address on polygon
* **contract\_function\_signature:** swan payment gateway's lock payment event's function signature on polygon
* **dao\_swan\_oracle\_address:** swan dao address on polygon
* **dao\_event\_function\_signature:** swan dao's signature event's function signature on polygon
* **scan\_step:** the number of blocks scanned per scan
* **start\_from\_blockNo:** scan data from this block number
* **start\_from\_blockNo:** the time between each scan of the blockchain





**Want to learn more? Check out the** [**open source code**](https://github.com/filswan/payment-bridge) **and** [**API**](../development-resource/mcp-api.md)**. Join the team on** [**Discord**](https://discord.gg/djsVYe4b)**.**

### &#x20;<a href="#setup-local-geth-and-rollup-blockchain" id="setup-local-geth-and-rollup-blockchain"></a>

### &#x20;<a href="#hello-arbitrum" id="hello-arbitrum"></a>
