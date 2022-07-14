---
description: 本指南将解释如何安装 js-mcs-sdk 及其基本用法
---

# 开始

#### 先决条件 <a href="#xian-jue-tiao-jian-1" id="xian-jue-tiao-jian-1"></a>

* Node.js - 此 SDK 使用版本 v16.13.0 (npm v8.1.0) 构建
* Polygon Mumbai Testnet 钱包 - [Metamask Tutorial](https://docs.filswan.com/multi-chain-storage/mcp-user-guide/setup-metamask)
* Polygon Mumbai Testnet Alchemy RPC - [Alchemy Tutorial](https://docs.filswan.com/multi-chain-storage/mcp-user-guide/configure-metamask-with-alchemy-rpc-url#alchemypolygontometamaskinstructions-2.createalchemymumbaipolygonrpc)
* Mumbai Testnet USDC和 MATIC 也是必需的-[Swan Faucet Tutorial](https://docs.filswan.com/development-resource/swan-token-contract/acquire-testnet-usdc-and-matic-tokens)

#### 安装 <a href="#an-zhuang-1" id="an-zhuang-1"></a>

使用 npm 安装包。建议为新项目创建新目录。

```shell
npm init -y
npm install js-mcs-sdk
```

#### 环境变量 <a href="#huan-jing-bian-liang" id="huan-jing-bian-liang"></a>

获得Mumbai 测试网钱包和 RPC URL 后，创建一个名为 `.env`并存储你钱包的私钥和 RPC URL。

```shell
PRIVATE_KEY=<PRIVATE_KEY>
RPC_URL=https://polygon-mumbai.g.alchemy.com/v2/<API_KEY>
```

> 小心不要泄露这些信息
>
> 向他人透露您的私钥将使他们能够访问您的钱包

#### 上传文件示例 <a href="#shang-chuan-wen-jian-shi-li" id="shang-chuan-wen-jian-shi-li"></a>

这是一个将单个文件上传到 MCS 的简单示例。 新建了一个文件名为 `upload.js`

```shell
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

// set up js-mcs-sdk
const mcs = new mcsSDK({
  privateKey: process.env.PRIVATE_KEY,
  rpcUrl: process.env.RPC_URL,
})

async function main() {
  const testFile = JSON.stringify({ address: mcs.publicKey })
  const fileArray = [{ fileName: `${mcs.publicKey}.txt`, file: testFile }]

  const uploadResponse = await mcs.upload(fileArray)
  console.log(uploadResponse)
}

main()
```

使用命令 `node upload.js`运行代码。 此代码段创建 MCS SDK 实例，使用您的钱包地址创建 JSON 文件，并将文件上传到 MCS。

#### 文档说明 <a href="#wen-dang-shuo-ming" id="wen-dang-shuo-ming"></a>

此 SDK 的以下文档将假定您已实例化 MCS SDK。 使用 `mcs`以下示例的变量。

```shell
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

// set up js-mcs-sdk
const mcs = new mcsSDK({
  privateKey: process.env.PRIVATE_KEY,
  rpcUrl: process.env.RPC_URL,
})
```

并且所有以上片段将替换 `main()`上面的功能。
