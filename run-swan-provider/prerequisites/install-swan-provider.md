# Installation

ou can set the `$SWAN_PATH` by the environment variable, default `~/.swan`:

```
export SWAN_PATH="/data/.swan"
```

#### Option1️⃣ **Prebuilt package**: See [release assets](https://github.com/filswan/go-swan-provider/releases)

**Build Instructions**

```
wget --no-check-certificate https://raw.githubusercontent.com/filswan/go-swan-provider/release-2.1.0-rc1/install.sh
chmod +x ./install.sh
./install.sh
```

**Config and Run**

* Edit config file **\~/.swan/provider/config.toml**, configuration instruction is [here](../../swan-provider/prerequisites/configuration-and-run.md)
* Run `swan-provider` in the background

```
ulimit -SHn 1048576
export SWAN_PATH="/data/.swan"
nohup swan-provider-2.1.0-rc1-linux-amd64 daemon >> swan-provider.log 2>&1 & 
```

#### Option2️⃣ Source Code

Building the `swan-provider` requires some system dependencies:

```
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -
```

```
sudo apt-get install -y nodejs
```

```
sudo apt install mesa-opencl-icd ocl-icd-opencl-dev gcc git bzr jq pkg-config curl clang build-essential hwloc libhwloc-dev wget -y && sudo apt upgrade -y
```

* Go(required **1.18.1+**)

```
wget -c https://golang.org/dl/go1.18.1.linux-amd64.tar.gz -O - | sudo tar -xz -C /usr/local
```

```
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc && source ~/.bashrc
```

* Rustup

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

**Build Instructions**

```
git clone https://github.com/filswan/go-swan-provider.git
cd go-swan-provider
git checkout release-2.1.0-rc1
./build_from_source.sh
```
