# 自动竞价交易

当矿工被市场匹配器(Market Matcher)分配一个任务后，客户端需要使用在创建任务时提交到swan平台的信息发送自动竞价交易。

该步骤以无限循环模式执行，当存在满足以下条件的交易时，系统会连续发送自动竞价交易。

**条件**：

* 任务在swan平台中；
* task.is\_public=true
* task.is\_public=true
* task.status=Assigned
* task.miner 不是 null

```
./swan-client auto -out-dir [output_files_dir]
```



**此步骤中用到的命令参数：**

* \-out-dir(可选)：Swan交易最终的元数据文件会被生成到此路径下，当缺省时，默认使用\[sender].output\_dir，见配置文件

**此步骤用到的配置项：**

* \[sender].wallet, 见配置文件
* \[sender].relative\_epoch\_to\_main\_network, 见配置文件
* \[sender].output\_dir, 只有在命令中 -out-dir 被缺省时才会生效, 见配置文件
* \[main].api\_url, 见配置文件
* \[main].api\_key, 见配置文件
* \[main].access\_token, 见配置文件

**此步骤之后生成的文件：**

* \[task-name]-auto.csv: 为更新离线交易状态和填充离线dealCID而生成的CSV
* \[task-name]-auto-deals.csv: 基于下一步生成的\[task-name]-metadata.csv更新dealCID
* \[task-name]-auto-deals.json: 基于下一步生成的\[task-name]-metadata.json更新dealCID, 见离线交易

注意：

* 程序的日志文件位于./logs
* 为了防止退出系统时程序终止，可用如下方式运行：

```
nohup ./swan-client auto -out-dir [output_files_dir] >> swan-client.log 2>&1 &
```
