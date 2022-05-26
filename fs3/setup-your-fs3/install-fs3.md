# Install FS3

## Install PostgreSQL Database

#### PostgreSQL

A PostgreSQL database is required to be pre-built for FS3 server usage. Check [PostgreSQL Tutorial](https://www.postgresqltutorial.com/) on installation and connection instructions.&#x20;

**Install PostgreSQL on Ubuntu**

First, execute the following command to create the file repository configuration:

```
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
```

Second, import the repository signing key**:**

```
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
```

Third, update the package list:

```
sudo apt-get update
```

Finally, install the latest version of PostgreSQL:

```
sudo apt-get install postgresql
```

**Connect to the PostgreSQL database server via psql**

```
sudo -i -u postgres
```

Next, It’ll prompt for the password of the current user. You need to provide the password and hit the `Enter` keyboard.&#x20;

```
psql
```

You’ll access the postgres prompt like this:

```
postgres=#
```

To quit the PostgreSQL prompt, you run the following command:

```
postgres=# \q
```

This above command will bring you back to the postgres Linux command prompt.

```
postgres@ubuntu-dev:~$
```

To return to your regular system user, you execute the `exit` command like this:

```
postgres@ubuntu-dev:~$ exit
```

**Create PostgreSQL Database**

Create USER and PASSWORD as 'root'

```
sudo -u postgres psql
postgres=# create database fs3;                                                //create 'fs3' PostgreSQL database                                    
postgres=# create user root with encrypted password 'root';                    //create USER and PASSWORD as 'root'
postgres=# grant all privileges on database fs3 to root;                       //grant privileges
postgres=# \q                                                                  //logout postgres
```

## &#x20;Install From Source

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

&#x20;**Build up Tables in Postgresql Database**

```
bash db_setup.sh       
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
* **SWAN\_TOKEN** : A valid swan token is required for posting task on swan platform. It can be received after creating an account on [Filswan](https://www.filswan.com/). Check [Filswan APIs](https://documenter.getpostman.com/view/13140808/TWDZJbzV) for more details on how to get authorization token.
{% endhint %}

**Build up FS3 server**

```
make
```



## Run a Standalone FS3 Server

**Run the FS3 Server**

```
./minio server ~/fs3-data
```

**Access Key and Secret Key**

The FS3 deployment starts using default root credentials `minioadmin:minioadmin` but you can change it with your own credentials.

**Change your Access Key and Secret Key**

```
export MINIO_ROOT_USER= MY_FS3_ACCESS_KEY
export MINIO_ROOT_PASSWORD=MY_FS3_SECRET_KEY
```

If you change the credential, build up FS3 server again to make it take effect. Then re-run the fs3 server.

```
make
./minio server ~/fs3-data
```

## **Open** FS3 Browser

You can test the deployment using the FS3 Browser, an embedded web-based object browser built into FS3 Server. Point a web browser running on the host machine to [http://127.0.0.1:9000](http://127.0.0.1:9000/) and log in with the root credentials. You can use the Browser to create buckets, upload objects, send deals, retrieve data and browse the contents of the FS3 server.

You can also connect using any S3-compatible tool, such as the [FS3-mc](https://github.com/filswan/fs3-mc) commandline tool.
