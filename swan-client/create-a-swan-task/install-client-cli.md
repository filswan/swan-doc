# Install Swan Client Tool

## Prerequisite

* Lotus node

### Ubuntu

* install missing packages as required

### Mac

* install missing packages as required
* hwloc, such as\


```
brew install hwloc
```

* set path LIBRARY\_PATH to point to hwloc, such as

```
export LIBRARY_PATH=/opt/homebrew/Cellar/hwloc/2.6.0/lib
```

## Installation

#### Option1️⃣ **Prebuilt package**: See [release assets](https://github.com/filswan/go-swan-client/releases)

```
mkdir swan-client
cd swan-client
wget --no-check-certificate https://github.com/filswan/go-swan-client/releases/download/v2.0.0-rc1/install.sh
chmod +x install.sh
./install.sh
```

**Option2️⃣ Source Code**

🔔**go 1.16+** is required

```
git clone https://github.com/filswan/go-swan-client.git
cd go-swan-client
git checkout <release_branch>
./build_from_source.sh
```

### After Installation

* If you install from the source code, the binary file `swan-client` is under `./build` directory, you need to switch to it.

```
cd build
```

* Before executing, you should check your configuration in `~/.swan/client/config.toml` to ensure it is right.

```
vi ~/.swan/client/config.toml
```
