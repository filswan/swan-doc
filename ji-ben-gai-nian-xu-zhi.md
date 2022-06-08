# 基本概念须知

### 任务 <a href="#task" id="task"></a>

* 一个任务可以包含一个或多个Car文件
* 每个Car文件可以发送给一个或多个矿工
* 为任务中的每个Car文件设置矿工的接单模式
  * **Auto-bid**: `task.bid_mode=1`, 市场匹配器将基于声誉系统和任务中Car文件最大副本数量的需要，自动为每个Car文件分配矿工。
  * **Manual-bid**: `task.bid_mode=0`, 竞价人中标后，任务持有人需要向中标者发起任务(交易)。
  * **None-bid**: `task.bid_mode=2`, 需要将任务中每个Car文件发送给指定的矿工。
* 任务状态:
  * **Created**: 任务创建后，不管它是什么类型，它的初始状态都是`created`。
  *   **ActionRequired**: 自动竞价任务（也就是`task.bid_mode=1`）有一些信息缺失或无效：

      * MaxPrice:缺失或不是一个有效的数字
      * FastRetrieval: 缺失
      * Type: 缺失，或没有有效值

      🔔 需要解决上述问题，并将任务状态更改为`Created`，以便参与运行市场匹配器下一轮匹配中去。

### CAR文件 <a href="#task" id="task"></a>

* Car文件是发送给矿工的一个独立单元
* 每个Car文件可以发送给一个或多个矿工
* Car文件可将源文件通过Lotus、Graph-split或IPFS生成
* Car文件最大为64GB
* Car文件状态:
  * **Created**: 任务创建后，任务中所有Car文件都处于这种状态
  * **ActionRequired**:自动竞价任务（也就是`task.bid_mode=1`）有一些信息缺失或无效：
    * FileSize: 缺失或不是一个有效的数字
    * FileUrl: 缺失
    * StartEpoch: 缺失，或当前值无效、小于0或小于当前高度(currentEpoch)
    * PayloadCid: 缺失
    * PieceCid: 缺失
  * **Assigned**: 当其任务处于自动竞价模式时，即`task.bid_mode=1`，表示一个Car文件已经被市场匹配器自动分配给一些矿工。

### 离线交易 <a href="#offline-deal" id="offline-deal"></a>

* 离线交易是指将Car文件发送给矿工的交易
* 离线交易状态:
  * **Assigned**: 只有在自动竞价模式，即`task.bid_mode=1`，当一个Car文件被分配给一个矿工时，一个离线交易记录被创建，它的状态是`Assigned`。
  * **Created**: 对于所有的竞价模式，Car文件发送给矿工后，对应的交易状态为 `Created`.
  * **…**: 还有其他几种状态，由Swan Provider和Swan Platform生成和使用，它们对所有竞价模式的任务具有相同的含义。
* 这个工具的每一步都会生成一个JSON文件，其中包含如下所示的文件信息:

```
[
 {
  "Uuid": "",
  "SourceFileName": "srcFiles",
  "SourceFilePath": "[source file path]",
  "SourceFileMd5": "",
  "SourceFileSize": 5231342,
  "CarFileName": "bafybeidezzxpy3lrvzz2py56vasl7modkss4v56qwh67tzhetsn2qh3aem.car",
  "CarFilePath": "[car file path]",
  "CarFileMd5": "30fc76af655688cc6ef49bbb96ce938a",
  "CarFileUrl": "[car file url]",
  "CarFileSize": 5234921,
  "PayloadCid": "bafybeidezzxpy3lrvzz2py56vasl7modkss4v56qwh67tzhetsn2qh3aem",
  "PieceCid": "baga6ea4seaqfbtlhrfnzuhbmwnjw4a7ovtjijae32g25o56jcuidk2fdzrjgmoi",
  "StartEpoch": null,
  "SourceId": null,
  "Deals": null
 }
]
```

```
[
 {
  "Uuid": "072f8d4a-b79e-42b7-9452-3b8d1d41c11c",
  "SourceFileName": "",
  "SourceFilePath": "",
  "SourceFileMd5": "",
  "SourceFileSize": 0,
  "CarFileName": "",
  "CarFilePath": "",
  "CarFileMd5": "",
  "CarFileUrl": "[car file url]",
  "CarFileSize": 5234921,
  "PayloadCid": "bafybeidezzxpy3lrvzz2py56vasl7modkss4v56qwh67tzhetsn2qh3aem",
  "PieceCid": "baga6ea4seaqfbtlhrfnzuhbmwnjw4a7ovtjijae32g25o56jcuidk2fdzrjgmoi",
  "StartEpoch": null,
  "SourceId": 2,
  "Deals": [
   {
    "DealCid": "bafyreih2feyqpckrsmjnwgkm44el45obi3em7cjh7udkq6jgp4flkce6ra",
    "MinerFid": "t03354",
    "StartEpoch": 575856
   }
  ]
 }
]
```

* 在每个步骤中生成的这个JSON文件将在其下一步中使用，并可用于将来重建graph。
* 生成`Uuid`是为了将来建立索引
