# 基本概念须知

### 任务 <a href="#task" id="task"></a>

在Filswan项目中，一个任务可以包含一个或者多个离线交易。

📁任务类型：包括两种基本的任务类型：

* 公开任务：指公开竞价的交易集合，包括两种类型：
  * 自动竞价：自动竞价的任务会被自动分配给选中的存储提供者，这些存储提供者是基于信誉系统(reputation system)和市场匹配器(Market Matcher)筛选得到的。
  * 手动竞价：当出价人(Storage Provider)赢得竞价时，任务持有方（Client）需要发起手动竞价任务给获胜的一方(Storage Provider)。
* 私有任务：指客户端会发起一个私有任务(交易的集合)给特定的存储提供者。

_**​**_📁_**任务状态:**_

* **已创建**：表示该任务第一次在filswan平台上被成功创建，此状态与任务类型无关。
* **已分配**：表示该任务已经被用户分配给一个存储提供者，包括用户手动分配和被自动竞价模块----市场匹配器(Market Matcher) 两种情况。
*   **需操作**：表示该自动竞价任务(系统设置为bid\_mode=1, public\_deal=true)有部分信息缺失或者无效：

    * MaxPrice: 缺失或者是一个无效的数字
    * FastRetrieval: 缺失
    * Type: 缺失或者值无效
    * 该任务不包含离线交易

    🔔注意：必须要解决以上问题并且将任务状态修改为Created才能参与到市场匹配器(Market Matcher)下一轮的匹配中去。
* **交易已发送**：表示该任务中所有的离线交易已经被发送到分配给该任务的存储提供者；
* **异常过程**：表示该任务中只有部分交易(不是所有交易)被发送到分配给该任务的存储提供者。

### 离线交易 <a href="#offline-deal" id="offline-deal"></a>

* 每个离线交易包含了由客户端工具生成的car文件的信息
* 一个car文件的大小最多为64GiB
* 该工具的每一步完成后会生成一个JSON文件，其中包含的文件信息如下：

```
[
 {
  "Uuid": "261ac5ae-cfbb-4ae2-a924-3361075b0e60",
  "SourceFileName": "test3.txt",
  "SourceFilePath": "[source_file_dir]/test3.txt",
  "SourceFileMd5": "17d6f25c72392fc0895b835fa3e3cf52",
  "SourceFileSize": 43857488,
  "CarFileName": "test3.txt.car",
  "CarFilePath": "[car_file_dir]/test3.txt.car",
  "CarFileMd5": "9eb7d54ac1ed8d3927b21a4dcd64a9eb",
  "CarFileUrl": "http://[IP]:[PORT]/ipfs/Qmb7TMcABYnnM47dznCPxpJKPf9LmD1Yh2EdZGvXi2824C",
  "CarFileSize": 12402995,
  "DealCid": "bafyreiccgalsj2a3wtrxygcxpp2hfq3h2fwafh63wcld3uq5hakyimpura",
  "DataCid": "bafykbzacecpuzwmiaxc2u4r5bb7p3ukkhotmkfw4mfv3un6huvk6ctugowikq",
  "PieceCid": "baga6ea4seaqjcip2xh265h2pucvwxv7seeawm4gfksfua4zsbb24zujplzsukja",
  "MinerFid": "[miner_fid]",
  "StartEpoch": 1266686,
  "SourceId": 2
 }
]
```

* 在每一步中生成的JSON文件将会在下一步中使用，而且在以后可以用来重建文件图形
* uuid 是为了后期索引目的而生成的。
