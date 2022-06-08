# 手动交易

#### 选项1️⃣ **手动交易** <a href="#xuan-xiang-one-shou-dong-jiao-yi" id="xuan-xiang-one-shou-dong-jiao-yi"></a>

**前提条件**:

* `task can be found by uuid in JSON file from swan platform`
* `task.bid_mode=0`

```shell
./swan-client deal -json [path]/[task-name]-metadata.json -out-dir [output_files_dir] -miner [storage_provider_ids]
```

**此命令相关参数如下:**

* \-json(必选): JSON格式的元数据文件的完整路径, 见[离线交易](https://stackedit.io/app#Offline-Deal)
* \-out-dir(可选): Swan交易最终的元数据文件会被生成到此路径下，当缺省时，默认使用 `[sender].output_dir`. 见[配置文件](https://stackedit.io/app#Configuration)
* \-miner(Required):你想要发送Car文件的存储供应商id，如果有多个矿工，用逗号分隔，例如`f01276`或`t03354,f01276`。

**此步骤用到的配置项:**

* \[sender].wallet, 见[配置文件](https://stackedit.io/app#Configuration)
* \[sender].verified\_deal, 见[配置文件](https://stackedit.io/app#Configuration)
* \[sender].fast\_retrieval, 见[配置文件](https://stackedit.io/app#Configuration)
* \[sender].start\_epoch\_hours, 见[配置文件](https://stackedit.io/app#Configuration)
* \[sender].skip\_confirmation, 见[配置文件](https://stackedit.io/app#Configuration)
* \[sender].max\_price, 见[配置文件](https://stackedit.io/app#Configuration)
* \[sender].duration, 见[配置文件](https://stackedit.io/app#Configuration)
* \[sender].output\_dir, 只有在命令中缺省`-out-dir` 时使用, 见[配置文件](https://stackedit.io/app#Configuration)
* \[main].api\_url, 见[配置文件](https://stackedit.io/app#Configuration)
* \[main].api\_key, 见[配置文件](https://stackedit.io/app#Configuration)
* \[main].access\_token, 见[配置文件](https://stackedit.io/app#Configuration)

**此步骤之后生成的文件:**

* \[task-name]-deals.json: 基于上一步生成的\[task-name]-metadata.json更新dealCID, 见[离线交易](https://stackedit.io/app#Offline-Deal)
