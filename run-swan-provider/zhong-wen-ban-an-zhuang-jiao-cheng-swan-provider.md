# 中文版安装教程Swan Provider

## 介绍

Swan Provider 提供以下功能:

• 使用aria2 自动下载离线交易

• 下载完成后，使用lotus 节点导入交易

• 将交易状态同步到Swan 平台，使客户以及存储提供商实时了解状态进展

• 自动得到来自FilSwan 平台上的竞拍任务

• 存储提供商目前接单可以得到十倍增益

## 安装以及配置步骤

### 1. 前提条件

{% hint style="warning" %}
请确保你具备前提条件再执行后期安装过程
{% endhint %}

#### 1.1 Lotus Miner (存储提供商节点）

#### 1.2 aira2 安装

```
sudo apt install aria2
```

aira2 是一个下载工具，它的安装是用于把用户发的单下载到Swan Provider 运行的电脑/服务器

### 2. 安装

{% hint style="warning" %}
可以在以下2 种方式中选择任意一种，我们更加推荐选择一
{% endhint %}

#### 2.1 选择一 Prebuilt Package

```
wget https://github.com/filswan/go-swan-provider/releases/download/release-0.1.0/install.sh
chmod +x ./install.sh
./install.sh
```

#### 2.2 选择二Source Code (需要满足go 1.16+)

```
git clone https://github.com/filswan/go-swan-provider.git
cd go-swan-provider
git checkout <release_branch>
chmod +x ./buld_from_source.sh
./buld_from_source.sh
```

### 3.配置文件

{% hint style="info" %}
Swan Provider 可能会因为你没有配置文件而退出，在这种情况下你需要：
{% endhint %}

#### 3.1 如果你在安装中选择了第一个选项Prebuilt Package (无需执行3.2)

3.1.1. 修改配置文件

```
vi ~/.swan/provider/config.toml
```

3.1.2. 输入以下命令行执行Swan- Provider

```
./swan-provider -0.1.0-unix
```

#### 3.2 如果你在安装中选择了第二个选项Source Code(无需执行3.1)

3.2.1. 修改配置文件

```
vi ~/.swan/provider/config.toml
```

3.2.2. 输入以下命令行执行Swan- Provider

```
./build/swan-provider
```

### 4.说明

4.1. Log 日志文件在 ./logs 里面

4.2. 你可以在 ./swan-provider 前添加 nohup ，可以防止在登出logout 后出现挂起信号停止服务

4.3. 你可以在 ./swan-provider 前面或者后面添加 &，使程序在后台持续运行

### 5. 配置解释

#### **5.1. \[port] ] 端口**

默认值为 8888，如需要请自行更换端口值

#### 5.2. \[aria2]

aria2\_download\_dir: 离线单下载且等待导入的文件地址，一般无需更改

aria2\_host: aria2 服务器地址，一般无需更改

aria2\_port: Aria2 服务器端口，一般无需更改

aria2\_secret: 必须与 rpc-secure 在aria2.conf 的值统一，一般无需更改

#### 5.3. \[main]

api\_url: Swan 的API 地址 "https://api.filswan.com" 一般无需更改

:information\_source:miner\_fid: 你的存储服务商ID 号

import\_interval: 每个交易中间的导入时间间隔，600 秒/10 分钟，一般无需更改

scan\_interval: 在 Swan 平台上扫描所有正在进行的交易和更新状态的时间间隔，600 秒/10 分钟，一般无需更改

:information\_source:api\_key: 你的 api key. 可以从Swan 平台得到，打开[网址](https://www.filswan.com)，点击 "个人信息"->"开发人员设置". 如图所示

![](<../.gitbook/assets/Swan Provider 中文版安装教程(1).tiff>)

:information\_source:access\_token: 你的access token. 可以从Swan 平台得到，打开[网址](https://www.filswan.com)-> "个人信息"->"开发人员设置".

api\_heartbeat\_interval: 心跳检测的时间间隔，300 秒或者5 分钟，一般无需更改

#### 5.4 \[bid]用于设置自动竞拍

bid\_mode: 0-选择竞拍模式，设置为手动 ；1- 选择竞拍模式，设置为自动

expected\_sealing\_time: 设置期待封装时间，1920 epoch 或者16 小时，1epoch=30 秒。交易设置开始过早会有拒绝的风险。一般无需更改。

start\_epoch: 设置epoch 开始的时间，2880 epoch 或者24 hours.

auto\_bid\_task\_per\_day: 设置每天自动接受任务的上限数量。
