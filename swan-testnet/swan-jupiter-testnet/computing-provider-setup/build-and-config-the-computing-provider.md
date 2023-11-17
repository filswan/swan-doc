# Build and config the Computing Provider

Firstly, clone the code to your local:

```bash
git clone https://github.com/lagrangedao/go-computing-provider.git
cd go-computing-provider
git checkout v0.3.0
```

Then build the Computing provider follow the below steps:

```bash
make clean && make
make install
```

Update Configuration The computing provider's configuration sample locate in `./go-computing-provider/config.toml.sample`

```
cp config.toml.sample config.toml
```

Edit the necessary configuration files according to your deployment requirements. These files may include settings for the computing-provider components, container runtime, Kubernetes, and other services.

```toml
[API]
Port = 8085                                     # The port number that the web server listens on
MultiAddress = "/ip4/<public_ip>/tcp/<port>"    # The multiAddress for libp2p
Domain = ""                                     # The domain name

RedisUrl = "redis://127.0.0.1:6379"           # The redis server address
RedisPassword = ""                            # The redis server access password

[LOG]
CrtFile = "/YOUR_DOMAIN_NAME_CRT_PATH/server.crt"	# Your domain name SSL .crt file path
KeyFile = "/YOUR_DOMAIN_NAME_KEY_PATH/server.key"   	# Your domain name SSL .key file path

[LAG]
ServerUrl = "https://api.lagrangedao.org"     # The lagrangedao.org API address
AccessToken = ""                              # Lagrange access token, acquired from “https://lagrangedao.org  -> setting -> Access Tokens -> New token”


[MCS]
ApiKey = ""                                   # Acquired from "https://www.multichain.storage" -> setting -> Create API Key
BucketName = ""                               # Acquired from "https://www.multichain.storage" -> bucket -> Add Bucket
Network = "polygon.mainnet"                   # polygon.mainnet for mainnet, polygon.mumbai for testnet
FileCachePath = "/tmp"                        # Cache directory of job data

[Registry]                                    
ServerAddress = ""                            # The docker container image registry address, if only a single node, you can ignore
UserName = ""                                 # The login username, if only a single node, you can ignore
Password = ""                                 # The login password, if only a single node, you can ignore
```
