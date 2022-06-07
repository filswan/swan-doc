# 前提条件

### 特性

Swan Provider监听来自Swan平台的离线交易。提供以下功能：

* 使用aria2作为下载服务自动下载离线交易。
* 下载完成后使用lotus导入交易。
* 同步交易状态到 [Swan Platform](https://console.filswan.com/#/dashboard)，让客户端和矿工了解状态的实时变化。
* 来自FilSwan竞价市场的自动竞价任务。

### 前提

* lotus-miner
* aria2

#### 安装arial2

```
sudo apt install aria2
```

#### Lotus Miner 令牌生成

Lotus miner令牌用于为Swan Provider导入交易

```
lotus-miner auth create-token --perm write
```

注意，Lotus Miner需要在后台运行！生成的令牌位于`$LOTUS_MINER_PATH/token`

参考: [Lotus: API tokens](https://docs.filecoin.io/build/lotus/api-tokens/#obtaining-tokens)
