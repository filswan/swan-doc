# Prerequisites

* Golang 1.15+.
* Node Js 14.0+.
* PostgreSQL 10.19+.
  * A PostgreSQL database is required to be pre-built for FS3 server usage. Check [PostgreSQL Tutorial](https://www.postgresqltutorial.com) on installation and connection instructions.&#x20;
* IPFS 0.8.0+.
  * A running IPFS node is needed for CAR file generation and files uploading and storage. You can refer [IPFS Command-line Docs](https://docs.ipfs.io/install/command-line/#official-distributions) for installation instructions and configuration
* Lotus node 1.13
  * A running lotus node is needed for CAR file information generation, deals sending and deals retrieval. You can refer [Lotus Docs](https://lotus.filecoin.io/docs/set-up/install/) for installation instructions and configuration.&#x20;
  * A Lotus full node is not a must for FS3 server but if you do not have a lotus full node, a lite node which configured to connect to a full node is required. More information on how to use a [Lotus Lite node](https://lotus.filecoin.io/docs/set-up/lotus-lite/).
