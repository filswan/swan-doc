# Prerequisites

* Lotus-miner
* Aria2 Service

**Start Lotus-miner**

Before launching the `swan-provider`, you must ensure that `Lotus-miner` is running normally. and `Lotus-miner` token is necessary for importing deals.

```
lotus-miner auth create-token --perm write
```

Note that the `Lotus-miner` needs to be running in the background! The created token is located at `$LOTUS_MINER_PATH/token` Reference: [Lotus: API tokens](https://lotus.filecoin.io/reference/basics/api-access/)

**Aria2 Service**

```
sudo apt install aria2
```
