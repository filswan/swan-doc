# 自动竞价交易

#### 选项2️⃣ **自动竞价交易** <a href="#xuan-xiang-two-zi-dong-jing-jia-jiao-yi" id="xuan-xiang-two-zi-dong-jing-jia-jiao-yi"></a>

* 当矿工被市场匹配器(Market Matcher)分配一个Car文件后，客户端需要使用在 [创建任务](https://stackedit.io/app#Create-A-Task)时提交到swan平台的信息发送自动竞价交易
* 该步骤以无限循环模式执行，当存在满足以下条件的交易时，系统会连续发送自动竞价交易：

**条件**:

* `your tasks in swan`
* `task.bid_mode=1`
* `offline_deals.status=Assigned`

```shell
./swan-client auto -out-dir [output_files_dir]
```

**此命令相关参数如下:**

* \-out-dir(可选): Swan交易最终的元数据文件会被生成到此路径下，当缺省时，默认使用`[sender].output_dir`，见[配置文件](https://stackedit.io/app#Configuration)

**此步骤用到的配置项:**

* \[sender].wallet, 见[配置文件](https://stackedit.io/app#Configuration)
* \[sender].output\_dir, 只有在命令中 `-out-dir` 被缺省时才会生效, 见[配置文件](https://stackedit.io/app#Configuration)
* main].api\_url, 见[配置文件](https://stackedit.io/app#Configuration)
* \[main].api\_key, 见[配置文件](https://stackedit.io/app#Configuration)
* \[main].access\_token, 见[配置文件](https://stackedit.io/app#Configuration)

**此步骤之后每个任务生成的文件**:

* \[task-name]-auto-deals.json: 基于下一步生成的\[task-name]-metadata.json更新dealCID, 见[离线交易](https://stackedit.io/app#Offline-Deal)

**注意:**

* 程序的日志文件位于./logs
* 可以在`./swan-client` 前面加上`nohup` 来忽略HUP(挂起)信号，从而避免退出系统时程序终止。
* 可以在命令中添加 `>> swan-client.log`，让所有的日志输出到`swan-client.log`中。
* 您可以在命令末尾添加`&`，让程序在后台运行。
* 例如:

```shell
nohup ./swan-client auto -out-dir [output_files_dir] >> swan-client.log 2>&1 &
```
