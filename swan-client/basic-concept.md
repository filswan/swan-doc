# Basic Concept

### Task

* A task can contain one or multiple car files
* Each car file can be sent to one or multiple miners
* Methods to set miners for each car file in a task
  * **Auto-bid**: `task.bid_mode=1`, Market Matcher will automatically allocate miners for each car file based on the reputation system and the max copy number the task needs.
  * **Manual-bid**: `task.bid_mode=0`, After bidders win the bid, the task holder needs to propose the task to the winners.
  * **None-bid**: `task.bid_mode=2`, It is required to propose each car file of a task to a list of specified miners.
*   Task Status:

    * **Created**: After a task is created, its initial status is `Created` regardless of its type.
    *   **ActionRequired**: An autobid task, that is, `task.bid_mode=1`, has some information missing or invalid:

        * MaxPrice: missing, or is not a valid number
        * FastRetrieval: missing
        * Type: missing, or not having valid value

        🔔You need to solve the above problems and change the task status to `Created` to participate next run of Market Matcher.

    ####

    ### Car file

    * A car file is an independent unit to be sent to miners
    * Each car file can be sent to one or multiple miners
    * A car file is generated from source file(s) by Lotus, Graph-split, or Ipfs
    * The size of a car file can be up to 64GB.
    *   Car File Status:

        * **Created**: After a task is created, all its car files are in this status
        * **ActionRequired**: An autobid task, that is, `task.bid_mode=1`, its car file has something missing or invalid:
          * FileSize: missing, or is not a valid number
          * FileUrl: missing
          * StartEpoch: missing, or not have valid value, less than 0, or current epoch
          * PayloadCid: missing
          * PieceCid: missing
        * **Assigned**: When its task is in auto-bid mode, that is, `task.bid_mode=1`, a car file has been assigned to a list of miners automatically by Market Matcher.

        ### Offline Deal

        An offline Deal means the transaction that a car file is sent to a miner

        * Offline Deal Status:
          * **Assigned**: Only in auto-bid mode, that is `task.bid_mode=1`, when a miner is assigned to a car file, an offline deal record is created, and its status is `Assigned`.
          * **Created**: For all the bid modes, after a car file is sent to a miner, the related deal status is `Created`.
          * **...**: There are several other statuses, which are generated and used by Swan Provider and Swan Platform and they have the same meaning for tasks of all bid modes.
        * Every step of this tool will generate a JSON file that contains file(s) description like the one of below:



```
[
 {
  "Uuid": "",
  "SourceFileName": "srcFiles",
  "SourceFilePath": "[source file path]",
  "SourceFileMd5": "",
  "SourceFileSize": 5231342,
  "CarFileName": "bafybeidezzxpy3lrvzz2py56vasl7modkss4v56qwh67tzhetsn2qh3aem.car",
  "CarFilePath": "[car file path]",
  "CarFileMd5": "30fc76af655688cc6ef49bbb96ce938a",
  "CarFileUrl": "[car file url]",
  "CarFileSize": 5234921,
  "PayloadCid": "bafybeidezzxpy3lrvzz2py56vasl7modkss4v56qwh67tzhetsn2qh3aem",
  "PieceCid": "baga6ea4seaqfbtlhrfnzuhbmwnjw4a7ovtjijae32g25o56jcuidk2fdzrjgmoi",
  "StartEpoch": null,
  "SourceId": null,
  "Deals": null
 }
]
```

```
[
 {
  "Uuid": "072f8d4a-b79e-42b7-9452-3b8d1d41c11c",
  "SourceFileName": "",
  "SourceFilePath": "",
  "SourceFileMd5": "",
  "SourceFileSize": 0,
  "CarFileName": "",
  "CarFilePath": "",
  "CarFileMd5": "",
  "CarFileUrl": "[car file url]",
  "CarFileSize": 5234921,
  "PayloadCid": "bafybeidezzxpy3lrvzz2py56vasl7modkss4v56qwh67tzhetsn2qh3aem",
  "PieceCid": "baga6ea4seaqfbtlhrfnzuhbmwnjw4a7ovtjijae32g25o56jcuidk2fdzrjgmoi",
  "StartEpoch": null,
  "SourceId": 2,
  "Deals": [
   {
    "DealCid": "bafyreih2feyqpckrsmjnwgkm44el45obi3em7cjh7udkq6jgp4flkce6ra",
    "MinerFid": "t03354",
    "StartEpoch": 575856
   }
  ]
 }
]
```

* This JSON file generated in each step will be used in its next step and can be used to rebuild the graph in the future.
* Uuid is generated for future index purposes.
