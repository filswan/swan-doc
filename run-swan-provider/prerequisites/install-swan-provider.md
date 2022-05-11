# Install Swan Provider

**Option**1️⃣ **Prebuilt package**:

```
mkdir swan-provider
cd swan-provider
wget --no-check-certificate https://github.com/filswan/go-swan-provider/releases/download/v0.2.1/install.sh
chmod +x ./install.sh
./install.sh
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

#### 💥Important

After installation, Swan Provider may quit unexpectedly due to lack of configuration. Under this situation, you need

At the time of this writing, the latest release is **release-v0.2.1**

* 1️⃣ Edit config file **\~/.swan/provider/config.toml** to solve this.
* 2️⃣ Execute **swan-provider** using one of the following commands\


```
./swan-provider-0.2.1-linux-amd64   #After installation from Option 1
./build/swan-provider               #After installation from Option 2
```

```
./swan-provider-0.2.0-unix 
```

#### Note

* Logs are in directory ./logs
* You can add `nohup` before `./swan-provider` to ignore the HUP (hangup) signal and therefore avoid stop when you log out.
* You can add `>> swan-provider.log` in the command to let all the logs output to `swan-provider.log`.
* You can add `&` at the end of the command to let the program run in background.
* Such as:

```
nohup ./swan-provider-0.2.0-unix >> swan-provider.log &   #After installation from Option 1
```

```
nohup ./swan-provider-0.2.1-linux-amd64 >> swan-provider.log &   #After installation from Option 1
nohup ./build/swan-provider >> swan-provider.log &               #After installation from Option 2
```
