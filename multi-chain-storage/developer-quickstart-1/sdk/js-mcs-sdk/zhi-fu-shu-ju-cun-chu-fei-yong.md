---
description: 在 MCS 上支付存储费用
---

# 支付数据存储费用

```shell
makePayment(wCid, minAmount, fileSize)
```

上传文件后，文件可以按其有效负载 cid 付费。该方法将有效负载 cid 作为第一个参数，将最小数量作为第二个参数。

```shell
const W_CID = ''
const MIN_AMOUNT = '1'
const FILE_SIZE = ''
 
const tx = await mcs.makePayment(W_CID, MIN_AMOUNT, FILE_SIZE)
console.log(tx.transactionHash)
```

#### 参数 <a href="#can-shu-1" id="can-shu-1"></a>

* **wCid**：文件的唯一有效负载
* **minAmount**：为文件支付的最低金额。用于避免大数字精度错误的字符串值
* **fileSize**：文件的大小

#### 返回 <a href="#fan-hui-1" id="fan-hui-1"></a>

返回 web3.js接收对象。在上面的示例中，仅打印来自此对象的事务哈希。

\
