# Public Task

#### **1.** **Generate the public task**

A **public** task is a task you want the miners on Filecoin network bid for it.

in **config.toml**:&#x20;

`public_deal = true`

**Publish the public task**

```
python3 swan_cli.py task --input-dir [car_files_dir] --out-dir [output_files_dir] --name [task_name] --dataset [curated_dataset] --description [description]
```

**--input-dir (Required)** Input directory where the generated car files and car.csv are located

**--out-dir (optional)** Metadata CSV and Swan task CSV will be generated to the given directory. Default: `output_dir`specified in config.toml

**--name (optional)** Given task name while creating task on Swan platform. Default: swan-task-uuid

**--dataset (optional)** The curated dataset from which the Car files are generated

**--description (optional)** Details to better describe the data and confine the task or anything the storage provider needs to be informed

Two CSV files are generated after successfully running the command: task-name.csv, task-name-metadata.csv.

\[task-name.csv] is a CSV generated for posting a task on Swan platform or transferring to storage providers directly for offline import

```
uuid,miner_id,deal_cid,payload_cid,file_source_url,md5,start_epoch,piece_cid,file_size
```

\[task-name-metadata.csv] contains more content for creating proposal in the next step

```
uuid,source_file_name,source_file_path,source_file_md5,source_file_url,source_file_size,car_file_name,car_file_path,car_file_md5,car_file_url,car_file_size,deal_cid,data_cid,piece_cid,miner_id,start_epoch
```

#### **2. Propose offline deal to the bid winner**

Client needs to use the metadata CSV generated in the previous step for sending the offline deals to the miner.

```
python3 swan_cli.py deal --csv [metadata_csv_dir/task-name-metadata.csv] --out-dir [output_files_dir] --miner [storage_provider_id]
```

**--csv (Required):** File path to the metadata CSV file. Mandatory metadata CSV fields: source\_file\_size, car\_file\_url, data\_cid, piece\_cid

**--out-dir (optional):** Swan deal final CSV will be generated to the given directory. Default: output\_dir specified in config.toml

**--miner (Required):** Target storage provider id, e.g f01276

A csv with name \[task-name]-metadata-deals.csv is generated under the output directory, it contains the deal cid and storage provider id for the provider to process on Swan platform. You could re-upload this file to Swan platform while assign bid to storage provider or do a private deal.

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
