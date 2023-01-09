# Installation

## **From Prebuilt Package**

See [release assets](https://github.com/filswan/go-swan-client/releases)

```shell
mkdir swan-client
cd swan-client
wget --no-check-certificate https://github.com/filswan/go-swan-client/releases/download/v2.1.0-rc1/install.sh
chmod +x install.sh
./install.sh
```

## **From Source Code**

:bell:**go 1.16+** is required

```shell
git clone https://github.com/filswan/go-swan-client.git
cd go-swan-client
git checkout release-2.1.0-rc1
./build_from_source.sh
```

After you install from option two, the binary file `swan-client` is under the `./build` directory
