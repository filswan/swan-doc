# Install Swan Provider

#### Swan provider contains two major component

* A download utility(aria2)  for downloading .car files from remote server
* A .car file manager for managing importer process

### **Install aria2**

```
sudo apt install aria2
```

### Register your storage provider

You need to [Registering your storage provider](../../filswan-platform/core-modules/my-profile/swan-storage-provider/registering-your-storage-provider.md) before you can start bidding.

### Install Swan Provider Binary

The Swan Provider is a binary that is created from the [Swan Provider](https://github.com/filswan/go-swan-provider) repository.

It contains both the logic for running an Swan Provider and also provides a CLI for handling registry, staking and other operations.

```
wget https://github.com/filswan/go-swan-provider/releases/download/<release-version>/install.sh
chmod +x ./install.sh
sudo ./install.sh
```

{% hint style="warning" %}
The Swan Provider is currently only supported on x86\_64 Linux systems.
{% endhint %}

### Building From Source <a href="building-from-source" id="building-from-source"></a>

Although highly suggested, building from source is currently beyond the scope of this documentation.

See [go-swan-provider](https://github.com/filswan/go-swan-provider) documentation for more details.

The code in the [`main` branch](https://github.com/filswan/go-swan-provider/tree/main) might be incompatible with the code used by other nodes in the production.
