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
gateway_address = "/ip4/127.0.0.1/tcp/8080"

[sender]
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
```

**main**

Main section defines the token used for connecting with Swan platform. This part can be ignored if offline_mode is set to true in \[sender] section

* **api_key & access_token:** Acquire from [Filswan](https://www.filswan.com) -> "My Profile"->"Developer Settings". You can also check the [Guide](https://nebulaai.medium.com/how-to-use-api-key-in-swan-a2ebdb005aa4)
* **api_url:** Default: "[https://api.filswan.com](https://api.filswan.com)"

**web-server**

web-server is used to upload generated Car files. Miner will download Car files from this web-server. The downloadable URL in the CSV file is built with the following format: host+port+path+filename, e.g. [http://nbai.io:8080/download/](http://nbai.io:8080/download/)

**ipfs-server**

ipfs-server is used to upload generated Car files. Miner will download Car files from this ipfs-server. The downloadable URL in the CSV file is built with the following format: host+port+ipfs+hash, e.g. [http://host:port/ipfs/QmPrQPfGCAHwYXDZDdmLXieoxZP5JtwQuZMUEGuspKFZKQ](http://host/:port/ipfs/QmPrQPfGCAHwYXDZDdmLXieoxZP5JtwQuZMUEGuspKFZKQ)

**sender**

* **offline_mode:** \[true/false] Default false. If it is set to true, you will not be able to create Swan task on filswan.com, but you can still create CSVs and Car Files for sending deals
* **output_dir:** Output directory for saving generated Car files and CSVs
* **public_deal:** \[true/false] Whether deals in the tasks are public deals
* **verified_deal:** \[true/false] Whether deals in this task are going to be sent as verified
* **fast_retrieval:** \[true/false] Indicates that data should be available for fast retrieval
* **generate_md5:** \[true/false] Whether to generate md5 for each car file, note: this is a resource consuming action
* **skip_confirmation:** \[true/false] Whether to skip manual confirmation of each deal before sending
* **wallet:** Wallet used for sending offline deals
* **max_price:** Max price willing to pay per GiB/epoch for offline deal
* **start_epoch_hours:** start_epoch for deals in hours from current time
