# Get started

### Prerequisites

**Server Requirements**

Please see the hardware requirement below:

| Hardware | Provider Specifications     |
| -------- | --------------------------- |
| CPU      | 4-Core CPU with AVX support |
| RAM      | 8GB DDR4                    |
| Storage  | 500GB SSD                   |

**Install required software & set the configuration**

* lotus-miner
* aria2

#### arial2 installation

```
Lotus Miner Token creation
```

#### Lotus Miner Token creation

Lotus miner token is used for importing deal for swan provider

```
lotus-miner auth create-token --perm write
```

Note that the Lotus Miner needs to be running in the background! The created token is located at $LOTUS\_MINER\_PATH/token

Reference: [Lotus: API tokens](https://docs.filecoin.io/build/lotus/api-tokens/#obtaining-tokens)
