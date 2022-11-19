# Installation

#### Option1️⃣ **Prebuilt package**: See [release assets](https://github.com/filswan/go-swan-provider/releases)

**Build Instructions**

```
mkdir swan-provider
cd swan-provider
wget --no-check-certificate https://raw.githubusercontent.com/filswan/go-swan-provider/release-2.0.0/install.sh
chmod +x ./install.sh
./install.sh
```

**Config and Run**

* Edit config file **\~/.swan/provider/config.toml**, configuration instruction is [here](https://github.com/filswan/go-swan-provider/tree/release-2.0.0#Config)
* Run `swan-provider` in background

```
nohup ./swan-provider-2.0.0-linux-amd64 daemon >> swan-provider.log 2>&1 & 
```

#### Option2️⃣ Source Code

**Build Instructions**

```
git clone https://github.com/filswan/go-swan-provider.git
cd go-swan-provider
git checkout release-2.0.0
./build_from_source.sh
```

**Config and Run**

* Edit config file **\~/.swan/provider/config.toml**, configuration instruction is [here](https://github.com/filswan/go-swan-provider/tree/release-2.0.0#Config)
* Run `swan-provider` in background

```
nohup ./swan-provider daemon >> swan-provider.log 2>&1 & 
```

**Note:**

* Logs are in directory ./logs
* **go 1.16+** is required&#x20;
