# Basic Concepts

## 1. Task

A task can contain one or multiple CAR files. Each CAR file can be sent to one or multiple miners.&#x20;

## 2. Methods to set miners for each CAR file in a task

#### **2.1 Auto-bid**

`task.bid_mode=1`, Market Matcher will automatically allocate miners for each CAR file based on the [Reputation System](../swan-platform/overview/reputation-system.md) and the max copy number the task needs.

**2.2 Manual-bid**

`task.bid_mode=0`, After bidders win the bid, the task holder needs to propose the task to the winners.

#### 2.3 None-bid&#x20;

It is required to propose each car file of a task to a list of specified miners.

## 3. Task status

#### **3.1 Created**

After a task is created, its initial status is `Created` regardless of its type.

#### **3.2 ActionRequired**

An auto-bid task, that is, `task.bid_mode=1`, has some information missing or invalid:

* MaxPrice: missing, or is not a valid number
* FastRetrieval: missing
* Type: missing, or not having a valid value

🔔You need to solve the above problems and change the task status to `Created` to participate next run of Market Matcher.

## 4. CAR file

A CAR file is an independent unit to be sent to miners. Each CAR file can be sent to one or multiple miners. A CAR file is generated from source file(s) by Lotus, Graph-split, or IPFS. The size of a car file can be up to 64GB.

## 5. CAR file status

#### **5.1 Created**

After a task is created, all its car files are in this status

#### **5.2 ActionRequired**

An auto-bid task, that is, `task.bid_mode=1`, its car file has something missing or invalid:

* FileSize: missing, or is not a valid number
* FileUrl: missing
* StartEpoch: missing, or not have a valid value, less than 0, or current epoch
* PayloadCid: missing
* PieceCid: missing

#### **5.3 Assigned**

When its task is in auto-bid mode, that is, `task.bid_mode=1`, a CAR file has been assigned to a list of miners automatically by Market Matcher.

## 6. Offline deal

An offline Deal means the transaction that a car file is sent to a miner.

## 7. Offline deal status

#### **7.1 Assigned**

Only in auto-bid mode, that is, `task.bid_mode=1`, when a miner is assigned to a car file, an offline deal record is created, and its status is `Assigned`.

#### **7.2 Created**

For all the bid modes, after a car file is sent to a miner, the related deal status is `Created`.

#### **7.3 ...**

There are several other statuses, which are generated and used by Swan Provider and Swan Platform and they have the same meaning for tasks of all bid modes.



Every step of this tool will generate a JSON file that contains file(s) description like the one below:

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

This JSON file generated in each step will be used in its next step and can be used to rebuild the graph in the future.

Uuid is generated for future index purposes.
