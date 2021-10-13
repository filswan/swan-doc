# Setup Your Swan Provider



{% hint style="info" %}
Make sure you followed  [Prerequisites](broken-reference) before configuration
{% endhint %}

### **Step 1: **Obtain your API keys 

Get your [API keys](broken-reference)  so that Swan can authenticate your integration’s API requests.

### **Step 2: Run Aria2 as System Service**

**2.1: Install Aria2**

```
sudo apt install aria2
```

**2.2: Set-up Aria2**

```
# Make a directory
sudo mkdir /etc/aria2

# Change user authority to current user
sudo chown $USER:$USER /etc/aria2/

# Create a session file
touch /etc/aria2/aria2.session

# Checkout the source and install 
git clone https://github.com/filswan/go-swan-provider.git
cd go-swan-provider

# Copy config file and service file
cp config/aria2.conf /etc/aria2/
sudo cp aria2c.service /etc/systemd/system/

# Modify /etc/systemd/system/aria2c.service, set User & Group to value of $USER  
sudo vi /etc/systemd/system/aria2c.service

# Set to start Aria2 automatically
sudo systemctl enable aria2c.service

# Start Aria2
sudo systemctl start aria2c.service
```

**2.3: Check if Aria2 service is successfully started**

```
journalctl -u aria2c.service -f
```

:ballot_box_with_check: The Aira2 service will listen on certain port if installed and started correctly.

### Step 3: Compile Code

```
make   # generate binary file and config file to ./build folder
```

### Step 4: Start Swan Provider

```
cd build
./swan-provider
vi ~/.swan/provider/config.toml   # update configuration
```

Please make sure you have proper privilege to create the file.

You need to change the following filed in **configs**:

**\[Service]**

* user: put current user, you could use "echo"
* group: put current group

**\[port]**

* **port：** the port for restful api

**\[aria2]**

* **aria2\_download_dir:** Directory where offline deal files will be downloaded for importing
* **aria2\_host:** Aria2 server address
* **aria2\_port:** Aria2 server port
* **aria2\_secret:** Must be the same value as rpc-secure in aria2.conf

**\[main]**

* **api_url:** Swan API address. For Swan production, it is "[https://api.filswan.com](https://api.filswan.com)"
* **miner_fid:** Your filecoin Miner ID
* **import_interval:** 600 seconds or 10 minutes. Importing interval between each deal.
* **scan_interval:** 600 seconds or 10 minutes. Time interval to scan all the ongoing deals and update status on Swan platform.
* **api_key:** Your api key. Acquire from Filswan -> "My Profile"->"Developer Settings". You can also check the Guide.
* **access_token:** Your access token. Acquire from Filswan -> "My Profile"->"Developer Settings". You can also check the Guide.
* **api_heartbeat_interval:** 600 seconds or 10 minutes. Time interval to send heartbeat

**\[bid]**

* **bid_mode:** 0: manual, 1: auto
* **expected_sealing_time:** 1920 epoch or 16 hours. The time expected for sealing deals. Deals starting too soon will be rejected.
* **start_epoch:** 2880 epoch or 24 hours. Relative value to current epoch
* **auto_bid_task_per_day:** auto-bid task limit per day for your miner defined above

```
[main]
api_url = "https://api.filswan.com"
miner_fid = "f0xxxx"
expected_sealing_time = 1920    # 1920 epoch or 16 hours
import_interval = 600           # 600 seconds or 10 minutes
scan_interval = 600           # 600 seconds or 10 minutes
api_key = ""
access_token = ""
[aria2]
aria2_download_dir = "/path/to/download/"
aria2_conf = "/etc/aria2/aria2.conf"
aria2_host = "localhost"
aria2_port = "6800"
aria2_secret = "my_aria2_secret"
```
