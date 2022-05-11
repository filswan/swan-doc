# Get started

Swan Provider is designed to run on a machine with a lotus miner node. Check [lotus miner node](https://lotus.filecoin.io/tutorials/lotus-miner/run-a-miner/#lotus-node-setup) spec to make sure you meet the hardware requirements.

### Prerequisites

* lotus-miner
* aria2

#### arial2 installation

```
sudo apt install aria2
```

#### Lotus Miner Token creation

Lotus miner token is used for importing deals for swan provider

```
lotus-miner auth create-token --perm write
```

Note: the Lotus Miner needs to be run in the background! The created token will be located at $LOTUS\_STORAGE\_PATH/token

Reference: [Lotus: API tokens](https://docs.filecoin.io/build/lotus/api-tokens/#obtaining-tokens)
