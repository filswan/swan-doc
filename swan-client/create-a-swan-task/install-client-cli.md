# Install Swan Client Tool

## Code Repository

[https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1)

## Prerequisite

* Lotus node

## Installation

#### Option1️⃣ **Prebuilt package**: See [release assets](https://github.com/filswan/go-swan-client/releases)

```
mkdir swan-client
cd swan-client
wget https://github.com/filswan/go-swan-client/releases/download/v0.1.0-rc1/install.sh --no-check-certificate
chmod +x ./install.sh
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

* The binary file `swan-client` for Option2️⃣ is under `./build` directory, you need to switch to it.

```
cd build
```

* Before executing, you should check your configuration in `~/.swan/client/config.toml` to ensure it is right.

```
vi ~/.swan/client/config.toml
```
