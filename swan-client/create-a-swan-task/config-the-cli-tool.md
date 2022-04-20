# Config of Swan Client Tool

### **Configuration**

#### \[lotus]

* **client\_api\_url**: Url of lotus client web api, such as: **http://\[ip]:\[port]/rpc/v0**, generally the \[port] is **1234**. See [Lotus API](https://docs.filecoin.io/reference/lotus-api/#features)
* **client\_access\_token**: Access token of lotus client web api. It should have admin access right. You can get it from your lotus node machine using command `lotus auth create-token --perm admin`. See [Obtaining Tokens](https://docs.filecoin.io/build/lotus/api-tokens/#obtaining-tokens)

#### \[main]

* **api\_url**: Swan API address. For Swan production, it is "[https://api.filswan.com](https://api.filswan.com)". It can be ignored if `[sender].offline_mode=true`.
* ‼️**api\_key**: Your Swan API key. Acquire from [Swan Platform](https://www.filswan.com) -> "My Profile"->"Developer Settings". It can be ignored if `[sender].offline_mode=true`.
* ‼️**access\_token**: Your Swan API access token. Acquire from [Swan Platform](https://www.filswan.com) -> "My Profile"->"Developer Settings". It can be ignored if `[sender].offline_mode=true`.
* ‼️**storage\_server\_type**: "ipfs server" or "web server"

#### \[web-server]

* **download\_url\_prefix**: Web server url prefix, such as: `https://[ip]:[port]/download`. Store car files for downloading by storage provider. Car file url will be `[download_url_prefix]/[filename]`

#### \[ipfs-server]

* **download\_url\_prefix**: Ipfs server url prefix, such as: `http://[ip]:[port]`. Store car files for downloading by storage provider. Car file url will be `[download_url_prefix]/ipfs/[filename]`
* **upload\_url**: Ipfs server url for uploading files, such as `http://[ip]:[port]`

#### \[sender]

* **bid\_mode**: \[0/1] Default 1, which is auto-bid mod and it means swan will automatically allocate storage provider for it, while 0 is manual-bid mode and it needs to be bidded manually by storage providers.
* **offline\_mode**: \[true/false] Default false. When set to true, you will not be able to create a Swan task on filswan.com, but you can still generate Car Files, CSV and JSON files for sending deals.
* **output\_dir**: When you do not set -out-dir option in your command, it is used as the default output directory for saving generated car files, CSV and JSON files. You need have access right to this folder or to create it.
* **public\_deal**: \[true/false] Whether deals in this task are public or not.
* **verified\_deal**: \[true/false] Whether deals in this task are going to be sent as verified or not.
* **fast\_retrieval**: \[true/false] Indicates that data should be available for fast retrieval or not.
* **generate\_md5**: \[true/false] Whether to generate md5 for each car file and source file, note: this is a resource consuming action.
* **skip\_confirmation**: \[true/false] Whether to skip manual confirmation of each deal before sending.
* **wallet**: Wallet used for sending offline deals
* **max\_price**: Max price willing to pay per GiB/epoch for offline deals
* **start\_epoch\_hours**: Start\_epoch for deals in hours from current time.
* **expired\_days**: Expected completion days for storage provider sealing data.
* **gocar\_file\_size\_limit**: Go car file size limit in bytes
* **gocar\_folder\_based**: Generate car file based on whole folder, or on each file separately
* **duration**: Expressed in blocks (1 block is equivalent to 30s). Default value is 1512000, that is 525 days. Valid value range:\[518400, 1540000]. See [Make the Deal](https://docs.filecoin.io/store/lotus/store-data/#make-the-deal)
* **relative\_epoch\_from\_main\_network**: # Your network current epoch - main network current epoch
