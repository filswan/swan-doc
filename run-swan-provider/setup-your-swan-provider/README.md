# Setup Your Swan Provider

Setup Your Swan Provider Make sure you followed [Prerequisites](../prerequisites/) before configuration

### Step 1: Obtain your API keys

Get your[ API Keys](../../getting-started/authentication/api-keys.md) so that Swan can authenticate your integration’s API requests.

### Step 2: Start Swan Provider

Make sure your [Lotus miner](https://docs.filecoin.io/mine/lotus/) is running one the same machine as the Swan provider will communicate with it and cannot work otherwise.

```
./swan-provider
```

The first time start swan provider will be interrupted due to incorrect configuration.

Launching `swan-provider` creates a default configuration. The config file locations are platform specific:

* Linux:` ~/.swan/provider/config.toml`

### Step 3: update your config

edit `~/.swan/provider/config.toml `as follows

```
...
miner_fid = "f0xxxx"          # Your filecoin Miner ID
api_key = ""                  # Your api key. Acquire from Filswan -> "My Profile"->"Developer Settings". You can also check the Guide.
access_token = ""             # Your access token. Acquire from Filswan -> "My Profile"->"Developer Settings". You can also check the Guide.
...
```

### Step 4: Restart Swan Provider

```
./swan-provider
```

You should see the following logs if start successfully:

```
time="2021-10-12 18:55:09.153" level=info msg="Your config file is:/home/peware/.swan/provider/config.toml" func=InitConfig file="confi
g.go:46"
time="2021-10-12 18:55:09.212" level=info msg="Begin updating bid configuration" func=UpdateMinerBidConf file="swanClient.go:172"
time="2021-10-12 18:55:09.317" level=info msg="Bid configuration updated." func=UpdateMinerBidConf file="swanClient.go:196"
[GIN-debug] [WARNING] Creating an Engine instance with the Logger and Recovery middleware already attached.

[GIN-debug] [WARNING] Running in "debug" mode. Switch to "release" mode in production.
 - using env:	export GIN_MODE=release
 - using code:	gin.SetMode(gin.ReleaseMode)

[GIN-debug] GET  /api/v1/common/miner/host/info --> swan-provider/routers/commonRouters.GetSwanMinerVersion (4 handlers)
[GIN-debug] Listening and serving HTTP on :8888
time="2021-10-12 18:55:09.317" level=info msg=Start... func=aria2CheckDownloadStatus file="common.go:64"
time="2021-10-12 18:55:09.317" level=info msg=Start... func=aria2StartDownload file="common.go:73"
time="2021-10-12 18:55:09.317" level=info msg=Start... func=lotusStartScan file="common.go:91"
time="2021-10-12 18:55:09.317" level=info msg=Start... func=lotusStartImport file="common.go:82"
time="2021-10-12 18:55:09.317" level=info msg=Start... func=swanSendHeartbeatRequest file="common.go:55"
time="2021-10-12 18:55:09.563" level=info msg="{\n \"status\": \"success\"\n}\n" func=SendHeartbeatRequest file="swanService.go:26"
```
