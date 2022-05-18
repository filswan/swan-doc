# Basic Concept

### Task

In the Swan project, a task can contain one or multiple offline deal(s).

&#x20;_****_ :file\_folder:_**Task type: There are two basic types of tasks:**_

* **Public Task**: A deal set for open bid. It has 2 types:
  * Auto-bid: an auto-bid task will be automatically assigned to a selected storage provider based on reputation system and Market Matcher.
  * Manual-bid: after bidder winning the bid, the task holder needs to propose the manual-bid task to the winner.
* **Private Task**: It is required to propose deal(s) of a private task to a specified storage provider.

_****_:file\_folder:_**Task status:**_

* **Created**: A task is created successfully first time on Swan platform, regardless of its type.
* **Assigned**: A task has been assigned to a storage provider manually by users or automatically by auto-bid module: Market Matcher.
*   **ActionRequired**: An autobid task, that is, `bid_mode=1` and `public_deal=true`, has some information missing or invalid:

    * MaxPrice: missing, or is not a valid number
    * FastRetrieval: missing
    * Type: missing, or not have valid values
    * No offline deal for this task.

    🔔You need to solve the above problems and change the task status to `Created` to participate next run of Market Matcher.
* **DealSent**: All offline deal(s) of this task has(have) been sent to a storage provider which has been assigned to this task.
* **ProgressWithFailure**: Some and not all of the deals of the task have been sent to a storage provider which has been assigned to this task.

### Offline Deal

* Each offline deal contains information about a car file generated from the client tool.
* The size of a car file can be up to 64GB.
* Every step of this tool will generate a JSON file which contains file(s) description like below:

```
[
 {
  "Uuid": "261ac5ae-cfbb-4ae2-a924-3361075b0e60",
  "SourceFileName": "test3.txt",
  "SourceFilePath": "[source_file_dir]/test3.txt",
  "SourceFileMd5": "17d6f25c72392fc0895b835fa3e3cf52",
  "SourceFileSize": 43857488,
  "CarFileName": "test3.txt.car",
  "CarFilePath": "[car_file_dir]/test3.txt.car",
  "CarFileMd5": "9eb7d54ac1ed8d3927b21a4dcd64a9eb",
  "CarFileUrl": "http://[IP]:[PORT]/ipfs/Qmb7TMcABYnnM47dznCPxpJKPf9LmD1Yh2EdZGvXi2824C",
  "CarFileSize": 12402995,
  "DealCid": "bafyreiccgalsj2a3wtrxygcxpp2hfq3h2fwafh63wcld3uq5hakyimpura",
  "DataCid": "bafykbzacecpuzwmiaxc2u4r5bb7p3ukkhotmkfw4mfv3un6huvk6ctugowikq",
  "PieceCid": "baga6ea4seaqjcip2xh265h2pucvwxv7seeawm4gfksfua4zsbb24zujplzsukja",
  "MinerFid": "[miner_fid]",
  "StartEpoch": 1266686,
  "SourceId": 2
 }
]
```

* This JSON file generated in each step will be used in its next step and can be used to rebuild the graph in the future.
* Uuid is generated for future index purposes.

{% embed url="https://github.com/filswan/swan-client" %}
