# Prerequisites

### Prerequisites <a href="#prerequisites" id="prerequisites"></a>

**Server Requirements**

Please see the hardware requirement below:

| Hardware | Provider Specifications     |
| -------- | --------------------------- |
| CPU      | 4-Core CPU with AVX support |
| RAM      | 8GB DDR4                    |
| Storage  | 500GB SSD                   |

* lotus-miner
* aria2

#### Install Aria2 Service

```
sudo apt install aria2
```

#### Create Lotus Miner Token

Lotus miner token is used for importing deal for swan provider

```
lotus-miner auth create-token --perm write
```

Note that the Lotus Miner need to be running in the background! The created token located at `$LOTUS_MINER_PATH/token`

Reference: [Lotus: API tokens](https://lotus.filecoin.io/reference/basics/api-access/)
