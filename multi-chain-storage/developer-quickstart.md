# Developer Quickstart

Multi-Chain Storage (hereinafter called the 'MCS') is a suite of Ethereum scaling solutions that enables high-throughput, low cost smart contracts while remaining trustworthy secure.&#x20;

The following documentation describes how to use MCS, which is currently live on Polygon Mumbai Testnet. Whether you're a developer that just wants to start building or you're curious into digging deeper into the internals of MCS and how it works, this site is the right place for you.

## System Design

![](<../.gitbook/assets/image (29) (1).png>)

## How does MCS work? <a href="#how-does-arbitrum-work" id="how-does-arbitrum-work"></a>

If you're looking to discover how MCS works, the best place to begin is by the [User Guide](mcp-user-guide.md) section, which gives a high level overview of MCS's internals. From there, you can jump into more detailed explainers on various components of the system.

## Modules <a href="#__docusaurus" id="__docusaurus"></a>

**Token Swap:** Token Swap module is in charge of swap the user's token to wrapped token, it can be USDC or other tokens.

1. Users pay USDC or other tokens, which are called user tokens, when uploading a file.
2. MCS uses FIL, which is called wrapped token, to pay when store data to Filecoin network.
3. User tokens should be changed to wrapped token by this module and this step is called token exchange(swap).
4. Token exchange(swap) is done through Sushi Swap which is a DEX.

#### Payment Module:

1.  After a file is uploaded, the money to be paid is estimated based on the

    * the average price of all the swan **** miners;
    * file size;
    * duration;

    Then the estimated amount of money will be locked to the payment contract address, see [Configuration](https://github.com/filswan/multi-chain-payment#Configuration).
2. In unlock step, the amount pay to Filecoin network by swan platform FIL wallet, will be transferred to MCS payment receiver address, see [Configuration](https://github.com/filswan/multi-chain-payment#Configuration).
3. In refund step, the overpayment part that is locked will be returned to user wallet

**Swan Client API:** More information can be found [here](https://github.com/filswan/go-swan-client).

**DAO Signature:** If DAO detects that the file uploaded has been chained, it will trigger a signature operation

**Data DAO:** More information can be found at [Flink](https://github.com/filswan/flink).

**IPFS:** More information can be found **** [here](https://docs.ipfs.io).

**Filecoin Storage:** More information can be found [here](https://lotus.filecoin.io/docs/set-up/install/).

## How Can I Start Building <a href="#how-can-i-start-building" id="how-can-i-start-building"></a>

### Prerequisites

* OS: Ubuntu 20.04 LTS
* Mysql5.5+
* [Lotus Node](https://github.com/filswan/multi-chain-payment#Lotus-Node)
* [IPFS Client](https://docs.ipfs.io/install/)

#### Lotus Node

* Lotus node is used for making car files and sending offline deals.
* Install lotus node or louts lite node in the same machine as MCS.
* Lotus full node is too heavy compared with lotus lite node, so lotus lite node is preferred.
* Lotus lite node depends on a lotus node, so ensure that a lotus node exists somewhere when using lotus lite node.

**Option1️⃣** [**install a lotus full node**](https://lotus.filecoin.io/docs/set-up/install/)

**Option2️⃣** [**install a lotus lite node**](https://lotus.filecoin.io/docs/set-up/lotus-lite/#amd-and-intel-based-computers)

### Installation

#### Option1️⃣ **Prebuilt package**: See [release assets](https://github.com/filswan/multi-chain-payment/releases)

```
wget https://github.com/filswan/multi-chain-payment/releases/tag/v1.0.1/install.sh
./install.sh
```

#### Option2️⃣ Source Code

🔔**go 1.16+** is required

```
git clone https://github.com/filswan/multi-chain-payment.git
cd multi-chain-payment
git checkout <release_branch>
./build_from_source.sh
```

### After Installation

* Before executing, you should check your configuration in `~/.swan/mcp/config.toml` to ensure it is right.

```
vi ~/.swan/mcp/config.toml
```

* Before executing, you should check your enviornment variable in `~/.swan/mcp/.env` to ensure it is right.

```
vi ~/.swan/mcp/.env
```

* After set your config and env variable in the related files, you can run `multi-chain-payment` in `./build` directory.

```
./build/multi-chain-payment
```

#### Note

* Logs are in directory `./logs`
* You can add `nohup` before `./multi-chain-payment` to ignore the HUP (hangup) signal and therefore avoid stop when you log out.
* You can add `>> mcp.log` in the command to let all the logs output to `mcp.log`.
* You can add `&` at the end of the command to let the program run in background.
* Such as:

```
nohup ./multi-chain-payment-0.2.1-rc1-unix >> mcp.log &   #After installation from Option 1
nohup ./build/multi-chain-payment >> ./build/mcp.log &    #After installation from Option 2
```

### Configuration

You need to modify the config file and input your config params, the configuration items will be introduced below:

#### config.toml

* **port**: Web api port.
* **release**: When work in release mode: set this to true, otherwise to false and environment. variable GIN\_MODE not to release.
* **swan\_platform\_fil\_wallet**: The wallet address used to pay on the Filecoin network.
* **filink\_url**: Deals data can be searched from here.

**\[lotus]**

* **client\_api\_url**: URL of lotus client web api, such as: `http://[ip]:[port]/rpc/v0`, generally the `[port]` is `1234`. See [Lotus API](https://docs.filecoin.io/reference/lotus-api/#features)
* **client\_access\_token**: Access token of lotus client web api. It should have admin access right. You can get it from your lotus node machine using command `lotus auth create-token --perm admin`. See [Obtaining Tokens](https://docs.filecoin.io/build/lotus/api-tokens/#obtaining-tokens)

**\[ipfs\_server]**

* **download\_url\_prefix**: IPFS server url prefix, such as: `http://[ip]:[port]`. Store car files for downloading by storage provider. Car file url will be `[download_url_prefix]/ipfs/[file_hash]`
* **upload\_url\_prefix**: IPFS server url for uploading files, such as `http://[ip]:[port]`

**\[swan\_task]**

* **dir\_deal**: Output directory for saving generated Car files and CSVs.
* **verified\_deal**: \[true/false] Whether deals in this task are going to be sent as verified.
* **fast\_retrieval**: \[true/false] Indicates that data should be available for fast retrieval.
* **start\_epoch\_hours**: start\_epoch for deals in hours from current time.
* **expired\_days**: expected completion days for storage provider sealing data.
* **max\_price**: Max price willing to pay per GiB/epoch for offline deal.
* **generate\_md5**: \[true/false] Whether to generate MD5 for each car file, note: this is a resource consuming action.

**\[polygon]**

* **rpc\_url**: your polygon network RPC URL.
* **payment\_contract\_address**: swan payment gateway address on polygon to lock money.
* **sushi\_dex\_address**: sushi address on polygon.
* **usdc\_wFil\_pool\_contract**: address to get exchange rate between USDC and wFil from sushi on polygon.
* **dao\_contract\_address**: swan DAO address on polygon, to receive DAO signatures.
* **mcp\_payment\_receiver\_address**: MCS wallet address to receive money from unlock operation.
* **gas\_limit**: gas limit for transaction.
* **unlock\_interval\_minute**: unlock interval in minutes between 2 unlock operations, in cannot be less than 1.

#### .env

* **privateKeyOnPolygon**: private key of the wallet used to execute contract methods on the polygon network and pay for gas.





**Want to learn more? Check out the** [**open source code**](https://github.com/filswan/payment-bridge) **and** [**API**](../development-resource/mcp-api.md)**. Join the team on** [**Discord**](https://discord.gg/djsVYe4b)**.**

### &#x20;<a href="#setup-local-geth-and-rollup-blockchain" id="setup-local-geth-and-rollup-blockchain"></a>

### &#x20;<a href="#hello-arbitrum" id="hello-arbitrum"></a>
