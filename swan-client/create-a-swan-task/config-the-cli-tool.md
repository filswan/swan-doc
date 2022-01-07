# Config the CLI tool



In config.toml

```
[main]
api_key = ""
access_token = ""
api_url = "https://api.filswan.com"
storage_server_type = "ipfs server"

[web-server]
host = "https://nbai.io"
port = 443
path = "/download"

[ipfs-server]
upstream_url = "http://127.0.0.1:5001"
download_stream_url = "http://127.0.0.1:8080"

[sender]
bid_mode = 1
offline_mode = false
output_dir = "/tmp/tasks"
public_deal = true
verified_deal = true
fast_retrieval = true
skip_confirmation = false
generate_md5 = false
wallet = ""
max_price = "0"
start_epoch_hours = 96
expire_days = 4
```

**main**

Main section defines the token used for connecting with Swan platform. This part can be ignored if offline\_mode is set to true in \[sender] section

* **api\_key & access\_token:** Acquire from [Filswan](https://console.filswan.com/#/dashboard) -> "My Profile"->"Developer Settings". You can also check the [Guide](https://nebulaai.medium.com/how-to-use-api-key-in-swan-a2ebdb005aa4)
* **api\_url:** Default as "[https://api.filswan.com](https://api.filswan.com)"

**web-server**

web-server is used to upload generated Car files. Miner will download Car files from this web-server. The downloadable URL in the CSV file is built with the following format: host+port+path+filename, e.g. [http://nbai.io:8080/download/](http://nbai.io:8080/download/)

**ipfs-server**

ipfs-server is used to upload generated Car files. Miner will download Car files from this ipfs-server. The downloadable URL in the CSV file is built with the following format: host+port+ipfs+hash, e.g. [http://host:port/ipfs/QmPrQPfGCAHwYXDZDdmLXieoxZP5JtwQuZMUEGuspKFZKQ](http://host/:port/ipfs/QmPrQPfGCAHwYXDZDdmLXieoxZP5JtwQuZMUEGuspKFZKQ)

**sender**

* **bid\_mode:** \[0/1] Default 1. If it is set to 1, autobid mode is on which means public tasks posted will receive automatically bids from storage providers and tasks will be sent automatically after auto bids. In contrast, 0 represents the manual mode as public tasks need to be bid manually by storage providers and sent manually.
* **offline\_mode:** \[true/false] Default false. If it is set to true, you will not be able to create Swan task on filswan.com, but you can still create CSVs and Car Files for sending deals
* **output\_dir:** Output directory for saving generated Car files and CSVs
* **public\_deal:** \[true/false] Whether deals in the tasks are public deals
* **verified\_deal:** \[true/false] Whether deals in this task are going to be sent as verified
* **fast\_retrieval:** \[true/false] Indicates that data should be available for fast retrieval
* **generate\_md5:** \[true/false] Whether to generate md5 for each car file, note: this is a resource consuming action
* **skip\_confirmation:** \[true/false] Whether to skip manual confirmation of each deal before sending
* **wallet:** Wallet used for sending offline deals
* **max\_price:** Max price willing to pay per GiB/epoch for offline deal
* **start\_epoch\_hours:** start\_epoch for deals in hours from current time
* **expired\_days:** expected completion days for storage provider sealing data

****
