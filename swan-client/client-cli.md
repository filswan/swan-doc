# Client CLI



## Code Repository

[https://github.com/filswan/swan-client](https://github.com/filswan/swan-client)

## Client Tool Function List

* Encrypt and decrypt file with AES.
* Generate Car files from downloaded source files with or without Lotus.
* Generate metadata e.g. Car file URI, start epoch, etc. and save them to a metadata CSV file.
* Propose deals based on the metadata CSV file.
* Generate a final CSV file contains deal CIDs and miner id for miner to import deals.
* Create tasks on Swan Platform.

## Prerequisite

* Lotus node
* go 1.15+
* python 3.7+
* pip3

## Installation

#### Ubuntu/Debian

```
sudo apt-get update
sudo apt-get upgrade -y

# Install Git
sudo apt install git -y

# Checkout the source and install
git clone https://github.com/filswan/swan-client.git
cd swan-client

sh install.sh

. ./activate 
```

{% hint style="info" %}
&#x20;Make sure you have Prerequisite installed before you go to next step
{% endhint %}

## Config the deal server

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

{% hint style="info" %}
The **duration** time for offline deals is set to `1512000`epoches in default, which stands for 525 days.&#x20;

It can be further modified in constant `DURATION` of `swan-client/task_sender/service/deal.py` for customized requirement.
{% endhint %}

## Create Deal for Filecoin Network

### Prepare the data for sending deals

#### **Step 1: Generate Car files using Lotus (option 1)**

```
python3 swan_cli.py car --input-dir [input_files_dir] --out-dir [car_files_output_dir] 
```

{% hint style="info" %}
Note: The input dir and out dir shall only be in format of **Absolute Path.**
{% endhint %}

The output will be like:

```
INFO:root:Generating car file from: [input_file_dir]/ubuntu-15.04-server-i386.iso.tar
INFO:root:car file Generated: [car_files_output_dir]/ubuntu-15.04-server-i386.iso.tar.car, piece cid: baga6ea4seaqbpggkuxz7gpkm2wf3734gkyna3vb4p7bm3qcbl4gb4jgh22vj2pi, piece size: 15.88 GiB
INFO:root:Generating data CID....
INFO:root:Data CID: bafykbzacebbq4g73e4he32ahyynnamrft2tva2jyjt5fsxfqv76anptmyoajw
INFO:root:Car files output dir: [car_files_output_dir]
INFO:root:Please upload car files to web server or ipfs server.
```

If _`--out-dir` _ is not provided, then the output directory for the car files will be: ``` `_`output_dir`_ (specified in the configuration file) + random\_uuid

e.g. : /tmp/tasks/7f33a9d6-47d0-4635-b152-5e380733bf09

****

To use the generation locally, make sure go is available before starting.

Generate car files using golang

```
python3 swan_cli.py gocar --input-dir [input_files_dir] --out-dir [car_files_output_dir] 
```

#### Step 2: Upload Car files to web server or ipfs server

After the car files are generated, you need to copy the files to a web-server manually, or you can upload the files to local ipfs server.

If you decide to upload the files to local ipfs server:

```
python3 swan_cli.py upload --input-dir [input_file_dir]
```

The output will be like:

```
INFO:root:Uploading car file [car_file]
INFO:root:Car file [car_file] uploaded: https://OpenIpfsHost:Port/ipfs/QmPrQPfGCAHwYXDZDdmLXieoxZP5JtwQuZMUEGuspKFZKQ
```

#### Step 3. Create a task

In Filswan, deals are sending via task. A task contains serveral deals, each deal has their own data\_id, source file link, etc.

**Options 1: Private Task**

A private task is a task you have specific miner you want to send.

in  config.toml:&#x20;

`public_deal = false`

Send out the deal

```
python3 swan_cli.py task --input-dir [car_files_dir] --out-dir [output_files_dir] --miner [miner_id] --dataset [curated_dataset] --description [description]
```

The output will be like:

```
INFO:root:Swan Client Settings: Public Task: False  Verified Deals: True  Connected to Swan: True CSV/car File output dir: /tmp/tasks/[output_files_dir]
INFO:root:['lotus', 'client', 'deal', '--from', 't3u4othyfcqjiiveolvdczcww3rypxgonz7mnqfvbtf2paklpru5f6csoajdfz5nznqy2kpr4eielsmksyurnq', '--start-epoch', '547212', '--manual-piece-cid', 'baga6ea4seaqcqjelghbfwy2r6fxsffzfv6gs2gyvc75crxxltiscpajfzk6csii', '--manual-piece-size', '66584576', 'bafykbzaceb6dtpjjisy5pzwksrxwfothlmfjtmcjj7itsvw2flpp5co5ikxam', 't01101', '0.000000000000000000', '1051200']
INFO:root:wallet: t3u4othyfcqjiiveolvdczcww3rypxgonz7mnqfvbtf2paklpru5f6csoajdfz5nznqy2kpr4eielsmksyurnq
INFO:root:miner: t01101
INFO:root:price: 0
INFO:root:total cost: 0.000000000000000000
INFO:root:start epoch: 547212
Press Enter to continue...
INFO:root:Deal sent, deal cid: bafyreibnmon4sby7ibwiezcjgjge7mshl3h24vftzkab5fqm4ll2voarna, start epoch: 547212
INFO:root:Swan deal final CSV Generated: /tmp/tasks/[output_files_dir]/swan-client-demo-deals.csv
INFO:root:Refreshing token
INFO:root:Working in Online Mode. A swan task will be created on the filwan.com after process done. 
INFO:root:Metadata CSV Generated: /tmp/tasks/[output_files_dir]/swan-client-demo-metadata.csv
INFO:root:Swan task CSV Generated: /tmp/tasks/[output_files_dir]/swan-client-demo.csv
INFO:root:Creating new Swan task: swan-client-demo
INFO:root:New Swan task Generated.
```

**Options 2: Public Task**

A **public** task is a task you want the miners on Filecoin network bid for it.

**1. Generate the public task**

in **config.toml**:&#x20;

`public_deal = true`

**Publish the public task**

```
python3 swan_cli.py task --input-dir [car_files_dir] --out-dir [output_files_dir] --name [task_name] --dataset [curated_dataset] --description [description]
```

**--input-dir (Required)** Each file under this directory will be converted to a Car file, the generated car file will be located under the output folder defined in config.toml

**--out-dir (optional)** Metadata CSV and Swan task CSV will be generated to the given directory. Default: output\_dir specified in config.toml

**--name (optional)** Given task name while creating task on Swan platform. Default: swan-task-uuid

**--dataset (optional)** The curated dataset from which the Car files are generated

Two CSV files are generated after successfully running the command: task-name.csv, task-name-metadata.csv.

\[task-name.csv] is a CSV generated for posting a task on Swan platform or transferring to miners directly for offline import

```
uuid,miner_id,deal_cid,payload_cid,file_source_url,md5,start_epoch,piece_cid,file_size
```

\[task-name-metadata.csv] contains more content for creating proposal in the next step

```
uuid,source_file_name,source_file_path,source_file_md5,source_file_url,source_file_size,car_file_name,car_file_path,car_file_md5,car_file_url,car_file_size,deal_cid,data_cid,piece_cid,miner_id,start_epoch
```

**2. Propose offline deal to the bid winner**

Client needs to use the metadata CSV generated in the previous step for sending the offline deals to the miner.

```
python3 swan_cli.py deal --csv [metadata_csv_dir/task-name-metadata.csv] --out-dir [output_files_dir] --miner [storage_provider_id]
```

**--csv (Required):** File path to the metadata CSV file. Mandatory metadata CSV fields: source\_file\_size, car\_file\_url, data\_cid, piece\_cid

**--out-dir (optional)** Swan deal final CSV will be generated to the given directory. Default: output\_dir specified in config.toml

**--miner (Required):** Target miner id, e.g f01276

A csv with name \[task-name]-metadata-deals.csv is generated under the output directory, it contains the deal cid and miner id for miner to process on Swan platform. You could re-upload this file to Swan platform while assign bid to miner or do a private deal.

The output will be like:

```
INFO:root:['lotus', 'client', 'deal', '--from', 'f3ufzpudvsjqyiholpxiqoomsd2svy26jvy4z4pzodikgovkhkp6ioxf5p4jbpnf7tgyg67dny4j75e7og7zeq', '--start-epoch', '544243', '--manual-piece-cid', 'baga6ea4seaqcqjelghbfwy2r6fxsffzfv6gs2gyvc75crxxltiscpajfzk6csii', '--manual-piece-size', '66584576', 'bafykbzaceb6dtpjjisy5pzwksrxwfothlmfjtmcjj7itsvw2flpp5co5ikxam', 't01101', '0.000000000000000000', '1051200']
INFO:root:wallet: f3ufzpudvsjqyiholpxiqoomsd2svy26jvy4z4pzodikgovkhkp6ioxf5p4jbpnf7tgyg67dny4j75e7og7zeq
INFO:root:miner: t01101
INFO:root:price: 0
INFO:root:total cost: 0.000000000000000000
INFO:root:start epoch: 544243
Press Enter to continue...
INFO:root:Deal sent, deal cid: bafyreicqgsxql7oqkzr7mtwyrhnoedgmzpd5br3er7pa6ooc54ja6jmnkq, start epoch: 544243
INFO:root:Swan deal final CSV /tmp/tasks/[output_files_dir]/task-name-metadata-deals.csv
INFO:root:Refreshing token
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MTQzNzA5ODcsImlhdCI6MTYxNDI4NDU4Nywic3ViIjoiV2pIVkJDYWIxM2FyUURlUldwbkw0QSJ9.Hn8f0z2Ew6DuL2E2ELgpi9_Gj8xrg28S3v31dTUW32s
INFO:root:Updating Swan task.
INFO:root:Swan task updated.
```

#### Step 4. Auto send auto-bid mode tasks with deals to auto-bid mode storage provider

The autobid system between swan-client and swan-provider allows you to automatically send deals to a miner selected by Swan platform. All miners with auto-bid mode on have the chance to be selected but only one will be chosen based on Swan reputation system and Market Matcher. You can choose to start this service before or after creating tasks in Step 3. Noted here, only tasks with `bid_mode` set to `1` and `public_deal` set to `true` will be considered. A log file will be generated afterwards.

Start the autobid module:

```
python3 swan_cli_auto.py auto --out-dir [output_file_dir]
```

or (Recommanded)

```
nohup python3 swan_cli_auto.py auto --out-dir [output_file_dir] >> auto_deal.log &
```

**--out-dir (optional):** A deal info csv containing information of deals sent and a corresponding deal final CSV with deals details will be generated to the given directory. Default: `output_dir` specified in config.toml

The output will be like:

```
INFO:root:Getting My swan tasks info
INFO:root:Swan task count 203
INFO:root:Getting Swan task status, uuid: 9c330c9-ba7-4989-b0a-7b9f26602
INFO:root:Swan task status is: {"task_uuid": "9c330c9-ba7-4989-b0a-7b9f26602", "task_status": "Assigned", "deals": [{"contract_id": "0x5210ED929B5BEdBFFBA", "created_at": "1632762298", "deal_cid": null, "file_name": null, "file_path": null, "file_size": "103125", "file_source_url": "http://192.168.88.41:5050/ipfs/QmZAiNYWX8giAYnUrZXVowtBwVktKL8meBjf", "id": 6861, "md5_origin": "", "miner_id": null, "note": null, "payload_cid": "bafk2bzacebjglrfqg3eexbntnhke2zysfmdwkfnlankhq72fca3w2c", "piece_cid": "baga6ea4seaqa2nfklf5xgom5jelt75czi3i5ynhiwm2b5w3xfs", "start_epoch": 1160167, "status": "Created", "task_id": 1596, "updated_at": "1632762298", "user_id": 184}], "task": {"bid_mode": 1, "created_on": "1632762298", "curated_dataset": null, "description": null, "expire_days": 4, "fast_retrieval": 1, "is_public": 1, "max_price": "0.050000000000000000", "min_price": null, "miner_id": "t03354", "status": "Assigned", "tags": null, "task_file_name": "test.csv", "task_id": 1596, "task_name": "2021092702", "type": "regular", "updated_on": "\ufffd", "uuid": "9c3b30c9-ba17-4989-b03a-7b9f26602036"}}
INFO:root:['lotus', 'client', 'deal', '--from', 't3u7pumush376xbytsgs5wabkhtadjzfydxxda2vzyasg7cimkcphswrq66j4dubbhwpnojqd3jie6ermpwvvq', '--start-epoch', '320167', '--fast-retrieval=true', '--verified-deal=false', '--manual-piece-cid', 'baga6ea4seaqa2nfklf5xgom5jelt75czi3i5ynhiwm2b5w3xfsp7thnkfzgnmdq', '--manual-piece-size', '130048', 'bafk2bzacebjglrfqg3eexbntnhke2zysfmdwkfnlankhq72fca3w2c2dqq5j2', 't01101, '0.000000000000000000', '1051200']
INFO:root:wallet: umush376xbyabkhtadjzfydxxda2vzyasg7cimkcphswrq66j4dubbh
INFO:root:miner: t01101
INFO:root:price: 0
INFO:root:total cost: 0.000000000000000000
INFO:root:start epoch: 320167
INFO:root:fast-retrieval: true
INFO:root:verified-deal: false
INFO:root:Deal sent, deal cid: bafyrei2yuidanaxzsp3yvypxub5worfei5tojb55fd, start epoch: 320167
INFO:root:Swan deal info CSV Generated: /tmp/tasks/[output_files_dir]/task-uuid-info.csv
INFO:root:Swan deal final CSV /tmp/tasks/[output_files_dir]/task-uuid-deals.csv
INFO:root:Refreshing token
INFO:root:Updating Swan task.
INFO:root:Swan task updated.
```

{% hint style="info" %}
A successful autobid task will go through three major status - **`Created`,`Assigned`** and **`DealSent`**. The task status **`ActionRequired`** exists only when public task with autobid mode on failed in meeting the requirements of autobid. To avoid being set to **`ActionRequired`, a task must** be created or modified to have valid tasks and corresponding deals information as following.
{% endhint %}

*   **For task**:

    **task price:** Max price willing to pay per GiB/epoch for offline deal,which can be changed in `max_price` of `config.toml`

    **task fast retrieval:** \[true/false] Indicates that data should be available for fast retrieval,which can be changed in `fast_retreval` of `config.toml`

    **task type:** \[true/false] Whether deals in the tasks are public deals, which can be changed in `fast_retreval`of `config.toml`
*   **For deals**:

    **valid deals:** There must be at least one valid corresponding deal record. Check the \[task-name.csv] to make sure of it.

    **start epoch:** Start epoch for deals in hours from current time is also needed, which can be changed in `start_epoch_hours` of `config.toml`

    **car file urls:** The valid downloading url of car files must be filled in before creating Swan tasks. Check column `car_file_url` of car.csv before sending and modify it if needed.

    **car file size:** A correct car file size should be filled in \[car.csv] after car files generation

    **Payload Cid:** Also known as data cid, which should be given in \[car.csv] after car files generation.

    **Piece Cid:** Piece cid is required for offline deals,which should be given in \[car.csv] after car files generation as well.
