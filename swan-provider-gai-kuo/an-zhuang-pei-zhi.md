# 安装配置

### 安装

#### 选择1️⃣ **与构建软件包**: 参照 [release assets](https://github.com/filswan/go-swan-provider/releases) <a href="#xuan-ze-one-yu-gou-jian-ruan-jian-bao-can-zhao-releaseassets" id="xuan-ze-one-yu-gou-jian-ruan-jian-bao-can-zhao-releaseassets"></a>

```
mkdir swan-provider
cd swan-provider
wget --no-check-certificate https://github.com/filswan/go-swan-provider/releases/download/v2.0.0-rc1/install.sh
chmod +x ./install.sh
./install.sh
```

#### 选择2️⃣ 从源代码构建

🔔 需要 **go 1.16+**

```
git clone https://github.com/filswan/go-swan-provider.git
cd go-swan-provider
git checkout <release_branch>
./build_from_source.sh
```

#### ‼️ 重要事项

安装后，swan-provider可能会由于缺少配置文件而退出。此时，需要

* 1️⃣ 通过编辑配置文件 **\~/.swan/provider/config.toml** 来解决
* 2️⃣ 用下面其中一个命令执行 **swan-provider**

```
./swan-provider-2.0.0-rc1-linux-amd64 daemon  #从选择1安装完以后
./build/swan-provider daemon                  #从选择2安装完以后
```

* 日志位于 ./logs
* 你可以在`./swan-provider` 前面加上`nohup` 用来忽略HUP(挂起)信号，从而避免注销时停止。
* 你可以在命令中添加`>> swan-provider.log` 让所有日志输出到`swan-provider.log`.
* 您可以在命令末尾添加`&`，让程序在后台运行。
* 例如：

```
nohup ./swan-provider-2.0.0-rc1-linux-amd64 daemon >> swan-provider.log 2>&1 &   #从选择1安装完以后
nohup ./build/swan-provider daemon >> swan-provider.log 2>&1 &                   #从选择2安装完以后
```

### 配置 <a href="#pei-zhi" id="pei-zhi"></a>

* **port:** 默认 `8888`, 用于将来扩展的Web API端口
* **release:** ，默认 `true`, 当工作在release模式时，将此设置为true；否则设置为false，环境变量GIN\_MODE不释放

### \[lotus]

* ‼️**client\_api\_url:** lotus client web api的Url, 如: `http://[ip]:[port]/rpc/v0`, 一般 `[port]` 为 `1234`. 参照 [Lotus API](https://docs.filecoin.io/reference/lotus-api/)
* ‼️**market\_api\_url:** lotus market web api的Url, 如:`http://[ip]:[port]/rpc/v0`, 一般`[port]` 为 `2345`. 当market和miner没有分离时，这也是miner的web api的url。参照 [Lotus API](https://docs.filecoin.io/reference/lotus-api/)
* ‼️**market\_access\_token:** lotus market web api访问令牌。当market和miner没有分离时，这也是miner访问令牌的访问令牌。参照 [Obtaining Tokens](https://docs.filecoin.io/build/lotus/api-tokens/#obtaining-tokens)

#### \[aria2] <a href="#aria2" id="aria2"></a>

* **aria2\_download\_dir:** 离线交易文件进行下载以供导入的目录
* **aria2\_host:** Aria2 服务器地址
* **aria2\_port:** Aria2 服务器端口
* **aria2\_secret:** 必须与 `aria2.conf` 的rpc-secret值相同

#### \[main] <a href="#main" id="main"></a>

* **api\_url:** Swan API 地址. 对于Swan产品而言，则为 `https://go-swan-server.filswan.com`
* ‼️**miner\_fid:** filecoin 矿工 ID
* **import\_interval:** 600 秒 10 分钟. 每笔交易之间的导入间隔.
* **scan\_interval:** 600 秒 10 分钟. 在Swan平台上扫描所有正在进行的交易并更新状态的时间间隔。
* ‼️**api\_key:** 你的 api key. 可以通过 [Swan Platform](https://console.filswan.com/#/dashboard) -> “My Profile”->“Developer Settings” 获得. 你也可以访问操作指南.
* ‼️**access\_token:** 你的访问令牌. 可以通过 [Swan Platform](https://console.filswan.com/#/dashboard) -> “My Profile”->"Developer Settings"获得. 你也可以访问操作指南.
* **api\_heartbeat\_interval:** 300秒或5分钟。发送heartbeat的时间间隔。

#### \[bid] <a href="#bid" id="bid"></a>

* **bid\_mode:** 0: 手动, 1: 自动
* **expected\_sealing\_time:** 1920 epoch 或16小时。达成交易的预期时间。过早开始交易将被拒绝。
* **start\_epoch:** 2880 epoch或24小时。当前epoch的相对值。
* **auto\_bid\_deal\_per\_day:** 上述定义的矿工每天的自动竞价任务限制。

## 常见的问题和解决方案 <a href="#chang-jian-de-wen-ti-he-jie-jue-fang-an" id="chang-jian-de-wen-ti-he-jie-jue-fang-an"></a>

*   `My aria is not downloaded`

    请检查 aria2 是否正在运行

    ```shell
    ps -ef | grep aria2
    ```
*   `error msg="no response from swan platform”`

    请检查你的API endpiont 是否正确，应该是 `https://go-swan-server.filswan.com`

\
许可证

[Apache](https://github.com/filswan/go-swan-provider/blob/main/LICENSE)
