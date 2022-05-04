# Install Swan Provider

Swan provider contains two major component

* A download utility aria2 for downloading .car files from the remote server and Lotus Miner Token creation  for importing deals
* A .car file manager for managing the importer process

## 1. Install **Prerequisites**&#x20;

### **1.1 Install aria2**

### Lotus Miner Token creation

```
sudo apt install aria2
```

```
lotus-miner auth create-token --perm write
```

### 1.2 Lotus miner token creation

{% hint style="info" %}
Note that the Lotus Miner needs to be running in the background!\
The created token is located at $LOTUS\_STORAGE\_PATH/token
{% endhint %}

## Install Swan Provider Binary

```
lotus-miner auth create-token --perm write
```

### 2.1 Register your storage provider

You need to [Register your Strorage Provider](../../filswan-platform/core-modules/my-profile/registering-your-storage-provider.md) before you can start bidding.

### 2.2 Install Swan Provider Binary

At the time of this writing, the latest release is **release-v0.2.1-rc2**

The Swan Provider is a binary that is created from the [Swan Provider](https://github.com/filswan/go-swan-provider/tree/release-0.2.0) repository.

#### Option1️⃣ **Prebuilt package**:

```
mkdir swan-provider
cd swan-provider
wget https://github.com/filswan/go-swan-provider/releases/download/<release_version>/install.sh
chmod +x ./install.sh
./install.sh
```

**Edit config file：**

```
~/.swan/provider/config.toml 
```

**Execute swan-provider**

```
./swan-provider-0.2.0-unix 
```

#### Option2️⃣ Source Code：&#x20;

{% hint style="info" %}
#### 🔔**go 1.16+** is required
{% endhint %}

```
git clone https://github.com/filswan/go-swan-provider.git
cd go-swan-provider
git checkout <release_branch>
./build_from_source.sh
```

**Edit config file：**

```
~/.swan/provider/config.toml 
```

**Execute swan-provider**

```
./build/swan-provider  
```

{% hint style="warning" %}
The Swan Provider is currently only supported on x86\_64 Linux systems.
{% endhint %}

### 2.3 Note

* Logs are in directory ./logs
* You can add `nohup` before `./swan-provider` to ignore the HUP (hangup) signal and therefore avoid stopping when you log out.
* You can add `>> swan-provider.log` in the command to let all the logs output to `swan-provider.log`.
* You can add `&` at the end of the command to let the program run in the background.

**Option**1️⃣&#x20;

```
nohup ./swan-provider-0.2.0-unix >> swan-provider.log &   #After installation from Option 1
```

#### Option2⃣️

```
nohup ./build/swan-provider >> swan-provider.log &        #After installation from Option 2
```
