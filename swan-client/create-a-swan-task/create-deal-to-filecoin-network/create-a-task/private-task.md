# Private Task



In Filswan, deals are sending via task. A task contains serveral deals, each deal has their own data\_id, source file link, etc.

**Options 1: Private Task**

A private task is a task you have specific miner you want to send.

in  config.toml:&#x20;

`public_deal = false`

Send out the deal

```
python3 swan_cli.py task --input-dir [car_files_dir] --out-dir [output_files_dir] --miner [Storage_provider_id] --dataset [curated_dataset] --description [description]
```

**--input-dir (Required)** Input directory where the generated car files and car.csv are located

**--out-dir (optional)** Metadata CSV and Swan task CSV will be generated to the given directory. Default: `output_dir`specified in config.toml

**--miner (Required)** Storage provider Id you want to send private deal to

**--dataset (optional)** The curated dataset from which the Car files are generated

**--description (optional)** Details to better describe the data and confine the task or anything the storage provider needs to be informed.

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
