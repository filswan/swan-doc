---
description: 数据提供商DAO 为 Filecoin 网络提供 Chainlink Oracle 服务
---

# Flink

### 介绍

Flink 是一个数据提供商 DAO，旨在为 Filecoin 网络提供 Chainlink Oracle 服务。 Flink 为想要将数据存储在 Filecoin 上的用户提供多链的交易信息。

### 什么是 Filecoin - Chainlink 数据提供者 <a href="#shen-me-shi-filecoinchainlink-shu-ju-ti-gong-zhe" id="shen-me-shi-filecoinchainlink-shu-ju-ti-gong-zhe"></a>

Filecoin 是以太坊、BSC 和 Polygon 等区块链用户在链下存储大规模数据的最佳选择。 用户可以通过发送交易从 Filecoin 网络上传和检索数据。 但是，如何生成跨链证明仍然没有解决，并且在用户的存储需求和 Fileocin 存储解决方案之间造成了差距。

External adapter 允许访问高质量数据，并实现将智能合约连接到高级 Web API 的极大灵活性。 使用 Chainlink external adapter ，用户可以在预言机节点运营商上查看他们的交易信息。



{% embed url="https://github.com/filswan/flink" %}

### 用例 <a href="#yong-li" id="yong-li"></a>

#### 使用USDC支付Polygon上NFT的文件存储费用 <a href="#shi-yong-usdc-zhi-fu-polygon-shang-nft-de-wen-jian-cun-chu-fei-yong" id="shi-yong-usdc-zhi-fu-polygon-shang-nft-de-wen-jian-cun-chu-fei-yong"></a>

在Filecoin网络上保存NFT的一般过程是：

* 在Polygon网络上锁定付款
* 将代币兑换给Filecoin代理者
* Filecoin 代理者发送NFT交易给Filecoin存储提供者
* 获取链上交易ID
* chainlink预言机向Polygon链进行广播证明
* 存储DAO公证人根据chainlink预言机提供的交易信息对数据进行签名
* NFT支付费用解锁到Filecoin代理者

![](<../../.gitbook/assets/flink image.png>)

### 设计结构 <a href="#she-ji-jie-gou" id="she-ji-jie-gou"></a>

作为 Flink 数据提供商的三个必备条件：

* 数据聚合器
* chainlink 外部适配器
* DATA DAO数据公证人

几个区块链扫描器将首先将数据聚合到一个统一的数据提供者。 然后带有预言机智能合约的chainlink外部适配器会将证明广播到目标区块链网络。 之后，数据公证人将根据链上预言机数据签署交易。 一旦从 Chainlink 预言机中继链上证明，付款即被执行。

### 数据聚合器 <a href="#shu-ju-ju-he-qi" id="shu-ju-ju-he-qi"></a>

当 FIlecoin 代理将数据发送到存储提供商时，数据存储过程即开始。 存储提供商需要接受交易并上传链上交易接受确认，这意味着交易正在进行中，并且将在 Filecoin 网络上生成交易 ID。

数据聚合器将扫描来自不同数据源的 Filecoin 交易信息，并将信息作为 API 接口发送。 检查扫描相关代码的 `数据`目录，典型的交易信息采用以下格式：

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

### **Chainlink** 外部适配器 **- DATA DAO**

数据聚合器获取交易信息后，下一步需要外部适配器为数据 DAO 公证人提供 API 访问。

有关如何构建和部署 External Adapter 的详细信息，请查看[adapter](https://github.com/filswan/flink/tree/main/adapter)

### **Data DAO** 公证人



Data DAO 公证人负责签署多重签名钱包，以便将资金解锁给 Filecoin 代理。

DAO 合约允许社区在 DAO 中添加或删除公证人。 DAO 公证人在签名前将遵循以下步骤：

* 通过`proposal_cid`获取`deal_id`
* 从 Chainlink Filecoin 适配器获取 deal\_id
  * 如果匹配触发 DAO 签名
    * 匹配客户端地址
    * 匹配 deal\_cid (proposal\_cid)
  * 否则，等待下一个检查周期

****
