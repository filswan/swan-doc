# Configuration

* **port:** Default `8888`, web API port for extension in future
* **release:** Default `true`, when work in release mode: set this to true, otherwise to false and environment variable GIN\_MODE not to release

### Lotus Miner configuration

Please set up your deal price on lotus miner,e.g.

```
lotus-miner storage-deals set-ask --price=0.00000001 --verified-price=0 --min-piece-size=4096Mib --max-piece-size=32Gib
```

For more information, please check [lotus mine deals](https://lotus.filecoin.io/storage-providers/operate/manage-storage-deals/#offline-deal-workflow)

### **Add configuration item**



If there is an old version of the Swan Provider running, you need to add the new parameter manually. You can reference [Readme](https://github.com/filswan/go-swan-provider/tree/release-0.2.1) on how to config them

#### \[lotus]

* ‼️**client\_api\_url:** Url of lotus client web api, such as: `http://[ip]:[port]/rpc/v0`, generally the `[port]` is `1234`. See [Lotus API](https://docs.filecoin.io/reference/lotus-api/)
* ‼️**market\_api\_url:** Url of lotus market web api, such as: `http://[ip]:[port]/rpc/v0`, generally the `[port]` is `2345`. When market and miner are not separate, it is also the url of miner web api. See [Lotus API](https://docs.filecoin.io/reference/lotus-api/)
* ‼️**market\_access\_token:** Access token of lotus market web api. When market and miner are not separate, it is also the access token of miner access token. See [Obtaining Tokens](https://docs.filecoin.io/build/lotus/api-tokens/#obtaining-tokens)

#### \[aria2]

* **aria2\_download\_dir:** Directory where offline deal files will be downloaded for importing
* **aria2\_host:** Aria2 server address
* **aria2\_port:** Aria2 server port
* **aria2\_secret:** Must be the same value as rpc-secret in `aria2.conf`

#### \[main]

* **api\_url:** Swan API address. For Swan production, it is "[https://api.filswan.com](https://api.filswan.com)"
* **miner\_fid:** Your filecoin Miner ID
* **import\_interval:** 600 seconds or 10 minutes. Importing interval between each deal.
* **scan\_interval:** 600 seconds or 10 minutes. Time interval to scan all the ongoing deals and update status on Swan platform.
* **api\_key:** Your api key. Acquire from [Swan Platform ](https://console.filswan.com/#/dashboard)-> "My Profile"->"Developer Settings". You can also check the Guide.
* **access\_token:** Your access token. Acquire from [Swan Platform](https://console.filswan.com/#/dashboard) -> "My Profile"->"Developer Settings". You can also check the Guide.
* **api\_heartbeat\_interval:** 300 seconds or 5 minutes. Time interval to send heartbeat.
* **purge\_interval:** 600 seconds or 10 minutes. Time interval to purge downloaded car files whose deal status are Completed, ImportFailed or DealExpired

#### \[bid]

* **bid\_mode:** 0: manual, 1: auto
* **expected\_sealing\_time:** 1920 epoch or 16 hours. The time expected for sealing deals. Deals starting too soon will be rejected.
* **start\_epoch:** 2880 epoch or 24 hours. The relative value to current epoch
* **auto\_bid\_task\_per\_day:** auto-bid task limit per day for your miner defined above

#### License

[Apache](https://github.com/filswan/go-swan-provider/blob/main/LICENSE)
