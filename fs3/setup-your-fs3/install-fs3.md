# Install FS3

## Install From Source

### Checkout source code

```
git clone https://github.com/filswan/fs3
cd fs3
git checkout <release_branch>
```

### Build the Source Code

**Build UI**

```
cd browser
npm install
npm run release
```

**Install Filecoin dependency**

```
sudo apt install mesa-opencl-icd ocl-icd-opencl-dev gcc git bzr jq pkg-config curl clang build-essential hwloc libhwloc-dev wget -y && sudo apt upgrade -
```

**Install go module dependency**

```
cd ..
git submodule update --init --recursive
make ffi
```

**Set up FS3 configuration**

Set up and customize FS3 configuration by making modifications on `.env` file, which stores your information as environment variables. An example config is given as `.env.example` for reference.

```
vim .env
```

{% hint style="info" %}
## Please Modify the `.env` file based on your use cases:

* **SWAN\_ADDRESS** : The address of filswan platform, default as `https://api.filswan.com`.
* **FS3\_VOLUME\_ADDRESS** : The address of FS3 VOLUME, default as `~/minio-data`. If changed, the FS3 server start command has to be changed accordingly.
* **FS3\_WALLET\_ADDRESS** : A wallet address is a must for sending deals to miner.
* **CAR\_FILE\_SIZE** : A fixed car file size in bytes need to be predefined before generating car files for trunk via variable `CarFileSize`, such as `8589934592` for 8Gb as default.
* **IPFS\_API\_ADDRESS** : An available ipfs address with port need to be set up. For example, `https://MyIpfsUrl:Port`.
* **IPFS\_GATEWAY** : An available ipfs address with port need to be set up for file downloading. For example, `https://MyIpfsGatewayUrl:Port`.
* **SWAN\_TOKEN** : A valid swan token is required for posting task on swan platform. It can be received after creating an account on [Filswan](https://www.filswan.com). Check [Filswan APIs](https://documenter.getpostman.com/view/13140808/TWDZJbzV) for more details on how to get authorization token.
{% endhint %}

**Build up FS3 server**

```
make
```



## Run a Standalone FS3 Server



```
 ./minio server ~/minio-data
```

The default FS3 volume address `Fs3VolumeAddress` is set as `~/minio-data`, which can be changed in `.env`. If the volume address is changed in the future, build up the FS3 server again to make the changes take effect.

The FS3 deployment starts using default root credentials `minioadmin:minioadmin`. You can test the deployment using the FS3 Browser, an embedded web-based object browser built into FS3 Server. Point a web browser running on the host machine to [http://127.0.0.1:9000](http://127.0.0.1:9000) and log in with the root credentials. You can use the Browser to create buckets, upload objects, send deals, retrieve data and browse the contents of the FS3 server.

You can also connect using any S3-compatible tool, such as the FS3 `mc` commandline tool.
