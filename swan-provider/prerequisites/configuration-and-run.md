# Configuration and Run

The configuration needs to be set according to the different `market_version`.

```
port = 8888
release = true                                  # when working in release mode: set this to true, otherwise to false and environment variable GIN_MODE not to release

[lotus]
client_api_url = "http://[ip]:[port]/rpc/v0"    # Url of lotus client web API, generally the [port] is 1234
client_api_token = ""                           # Access token of lotus client web API. (lotus auth api-info --perm=admin)
market_api_url = "http://[ip]:[port]/rpc/v0"   	# Url of lotus market web API, generally the [port] is 2345, when market and miner are not separate, it is also the URL of miner web API
market_access_token = ""                        # Access token of lotus market web API, when market and miner are not separate, it is also the access token of miner web API

[aria2]
aria2_download_dir = "%%ARIA2_DOWNLOAD_DIR%%"   # Directory where offline deal files will be downloaded for importing
aria2_candidate_dirs = ["/tmp"]			# Directories to find the CAR file required for the offline deal
aria2_host = "127.0.0.1"                        # Aria2 service address
aria2_port = 6800                               # Aria2 service port
aria2_secret = "my_aria2_secret"                # Must be the same value as RPC-secure in aria2.conf
aria2_auto_delete_car_file= false               # After the deal becomes Active or Error, the CAR file will be deleted automatically
aria2_max_downloading_tasks = 10                # Aria2 max downloading tasks. default: 10

[main]
market_version = "1.1"                          # Send deal type, 1.1 or 1.2, config(market_version=1.1) is DEPRECATION, will REMOVE SOON (default: "1.1"), If set to 1.2, you need to set the [market] section
api_url = "https://go-swan-server.filswan.com"  # Swan API address. For Swan production, it is "https://go-swan-server.filswan.com"
api_key = ""                                    # Your api key. Acquire from Filswan -> "My Profile"->"Developer Settings". You can also check the Guide.
access_token = ""                               # Your access token. Acquire from Filswan -> "My Profile"->"Developer Settings". You can also check the Guide.
miner_fid = "f0xxxx"                            # Your Filecoin MinerID, this miner must be added to the Swan Storage providers list by Swan Platform -> "My Profile" -> "As Storage Provider" -> "Manage" -> "Add"
import_interval = 600                           # 600 seconds or 10 minutes. Importing interval between each deal.
scan_interval = 600                             # 600 seconds or 10 minutes. Time interval to scan all the ongoing deals and update status on the Swan platform.
api_heartbeat_interval = 300                    # 300 seconds or 5 minutes. Time interval to send a heartbeat.

[bid]
bid_mode = 1                                    # 0: manual, 1: auto
expected_sealing_time = 1920                    # 1920 epoch or 16 hours. The time expected for sealing deals. Deals starting too soon will be rejected.
start_epoch = 2880                              # 2880 epoch or 24 hours. The relative value to current epoch
auto_bid_deal_per_day = 600                     # auto-bid deal limit per day for your miner defined above

[market]
collateral_wallet = ""                          # wallet to be used for deal collateral
publish_wallet = ""                             # wallet to be used for PublishStorageDeals messages
```

**(1) when `market_version = "1.1"`**, the storage provider will import deals using the Market built-in lotus, so the `[market]` section is not necessary to set.

**(2) when `market_version = "1.2"`**, the storage provider will import deals using the Market like `Boost`, so you must ensure the storage provider is reachable. The following steps are:

* Disable the markets subsystem in the miner config:

```
vi $LOTUS_MINER_PATH/config.toml
```

```
[Subsystems] 
 EnableMarkets = false
```

* Config the `[market]` section in the `$SWAN_PATH/provider/config.toml`
* Initialize the Market repo to the `$SWAN_PATH/provider/boost`:

```
export SWAN_PATH="/data/.swan"
swan-provider daemon 
```

*   Config the `[Libp2p]` section

    (1) Ensure that the `swan-provider` and `boostd` are not running

    ```
     kill -9 $(ps -ef | grep -E 'swan-provider|boostd' | grep -v grep | awk '{print$2}' )
    ```

    (2) Edit the boost configuration in the `$SWAN_PATH/boost/config.toml`:

    ```
     [Libp2p]
       ListenAddresses = ["/ip4/0.0.0.0/tcp/24001", "/ip6/::/tcp/24001"]   # Binding address for the libp2p host
       AnnounceAddresses = ["/ip4/209.94.92.3/tcp/24001"]                  # Addresses to explicitly announce to other peers. If not specified, all interface addresses are announced
    ```

    (3) Run `swan-provider` in the background.

    ```
     ulimit -SHn 1048576
     export SWAN_PATH="/data/.swan"
     nohup swan-provider daemon >> swan-provider.log 2>&1 & 
    ```
*   Publish Storage Provider's Multiaddrs and PeerID:

    * Acquired from `boostd --boost-repo=$SWAN_PATH/provider/boost net listen`

    ```
    lotus-miner actor set-addrs /ip4/<ip>/tcp/<port>   
    ```

    * Acquired from `boostd --boost-repo=$SWAN_PATH/provider/boost net id`

    ```
    lotus-miner actor set-peer-id <PeerID> 
    ```
* Set the storage provider's ask

```
export SWAN_PATH="/data/.swan"
swan-provider set-ask --price=0 --verified-price=0 --min-piece-size=256 --max-piece-size=34359738368
```

* Set the `[market].publish_wallet` as a control address:

```
export OLD_CONTROL_ADDRESS=`lotus-miner actor control list  --verbose | awk '{print $3}' | grep -v key | tr -s '\n'  ' '`
```

```
lotus-miner actor control set --really-do-it $[market].publish_wallet $OLD_CONTROL_ADDRESS
```

* Add funds to the `collateral_wallet` Market Actor

```
lotus wallet market add --from=<YOUR_WALLET> --address=<collateral_wallet> <amount>
```

> **Note:**
>
> * Logs are in the directory `./logs`
