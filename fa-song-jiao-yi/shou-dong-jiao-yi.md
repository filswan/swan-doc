# 手动交易

前提条件：

* 任务可以在filswan平台上通过JSON问津中的uuid找到
* task.is\_public=true
* task.bid\_mode=0

```
./swan-client deal -json [path]/[task-name]-metadata.json -out-dir [output_files_dir] -miner [storage_provider_id]
```

**此步骤中用到的命令参数：**

* \-json(必选)：JSON格式的元数据文件的完整路径，见离线交易
* \-out-dir(可选)：Swan交易最终的元数据文件会被生成到此路径下，当缺省时，默认使用\[sender].output\_dir，见配置文件
* \-miner(必选)：目标存储提供者ID，如f01276

**此步骤用到的配置项：**

* \[sender].wallet, 见配置文件
* \[sender].verified\_deal, 见配置文件
* \[sender].fast\_retrieval, 见配置文件
* \[sender].start\_epoch\_hours,见配置文件
* \[sender].skip\_confirmation, 见配置文件
* \[sender].max\_price, 见配置文件
* \[sender].duration, 见配置文件
* \[sender].relative\_epoch\_to\_main\_network, 见配置文件
* \[sender].output\_dir, 只有在命令中缺省-out-dir 时使用, 见配置文件
* \[main].api\_url, 见配置文件
* \[main].api\_key, 见配置文件
* \[main].access\_token, 见配置文件

**此步骤之后生成的文件：**

* \[task-name].csv: 为更新离线交易状态和填充离线dealCID而生成的CSV
* \[task-name]-deals.csv: 基于上一步生成的\[task-name]-metadata.csv更新dealCID
* \[task-name]-deals.json: 基于上一步生成的\[task-name]-metadata.json更新dealCID, 见离线交易
