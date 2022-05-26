# 安装配置

### 安装

#### 选择1️⃣ **预构建软件包**: 参照 [release assets](https://github.com/filswan/go-swan-provider/releases)

```
mkdir swan-provider
cd swan-provider
wget --no-check-certificate https://github.com/filswan/go-swan-provider/releases/download/v0.2.1/install.sh
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
./swan-provider-0.2.1-linux-amd64   #从选择一安装完以后
./build/swan-provider               #从选择二安装完以后
```

#### 注意

* 日志位于目录 ./logs
* 可以使用如下方式运行以防止程序退出，并将日志打印到单独的文件中：

```
nohup ./swan-provider-0.2.1-linux-amd64 >> swan-provider.log 2>&1 &   #从选择一安装完以后
nohup ./build/swan-provider >> swan-provider.log 2>&1 &               #从选择二安装完以后
```

### 配置

* **port：** 默认 `8888`，未来扩展的 web api 端口
* **release：** 默认为 `true`，在release模式下工作时设置为true；否则为false，此时环境变量`GIN_MODE`不会释放

#### \[lotus]

* ‼️**client\_api\_url:** lotus client web api的Url, 如: `http://[ip]:[port]/rpc/v0`, 一般 `[port]` 为 `1234`。 参照 [Lotus API](https://docs.filecoin.io/reference/lotus-api/)
* ‼️**market\_api\_url:** lotus market web api的Url, 如: `http://[ip]:[port]/rpc/v0`, 一般 `[port]` 为 `2345`。 当market和miner没有分离时，这也是miner的web api的url。参照 [Lotus API](https://docs.filecoin.io/reference/lotus-api/)
* ‼️**market\_access\_token:** lotus market web api访问令牌。当market和miner没有分离时，这也是miner访问令牌的访问令牌。参照 [Obtaining Tokens](https://docs.filecoin.io/build/lotus/api-tokens/#obtaining-tokens)

#### \[aria2]

* **aria2\_download\_dir:** 离线交易文件进行下载以供导入的目录
* **aria2\_host:** Aria2 服务器地址
* **aria2\_port:** Aria2 服务器端口
* **aria2\_secret:** 必须与 `aria2.conf` 的rpc-secret值相同

#### \[主要配置]

* **api\_url:** Swan API 地址 "[https://api.filswan.com"。](https://api.filswan.com"/)
* ‼️**miner\_fid:** filecoin 矿工 ID。
* **import\_interval:** 600秒或10分钟。每笔交易之间的导入间隔。
* **scan\_interval:** 600秒或10分钟。在Swan平台上扫描所有正在进行的交易并更新状态的时间间隔。
* ‼️**api\_key:** api key。可以通过 [Swan Platform](https://www.filswan.com/) -> "我的资料"->"开发者设置" 获得，也可以访问操作指南。
* ‼️**access\_token:** 访问令牌。可以通过 [Swan Platform](https://www.filswan.com/) -> "我的资料"->"开发者设置"获得，也可以访问操作指南。
* **api\_heartbeat\_interval:** 300秒或5分钟。发送心跳的时间间隔。
* **purge\_interval:** 600秒或10分钟。清除交易状态为“完成”、“导入失败”或“交易过期”的已下载的car文件的时间间隔。

#### \[竞价]

* **bid\_mode:** 0: 手动，1: 自动
* **expected\_sealing\_time:** 1920 epoch或16小时。达成交易的预期时间。过早开始交易将被拒绝。
* **start\_epoch:** 2880 epoch或24小时。当前epoch的相对值。
* **auto\_bid\_task\_per\_day:** 上述定义的矿工每天的自动竞价任务限制。

### 许可证

[Apache](https://github.com/filswan/go-swan-provider/blob/main/LICENSE)
