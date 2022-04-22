# Auto-bid Deal

### Option2️⃣ Auto-bid deal

* After a miner has been allocated to a task by Market Matcher, the client needs to send auto-bid deals using the information submitted to swan in step [Create A Task](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Create-A-Task).
* This step is executed in infinite loop mode, it will send auto-bid deals continuously when there are deals that can meet the below conditions.

**Conditions:**

* `your tasks in swan`
* `task.is_public=true`
* `task.bid_mode=1`
* `task.status=Assigned`
* `task.miner is not null`

```
./swan-client auto -out-dir [output_files_dir]
```

**Command parameters used in this step:**

* \-out-dir(optional): Swan deal final metadata files will be generated to the given directory. When ommitted, use default: `[sender].output_dir`. See [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)

**Configurations used in this step:**

* \[sender].wallet, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[sender].relative\_epoch\_to\_main\_network, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[sender].output\_dir, only used when -out-dir is omitted in command, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[main].api\_url, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[main].api\_key, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[main].access\_token, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)

**Files generated for each task after this step:**

* \[task-name]-auto.csv: A CSV generated for updating task status and fill deal CID for offline deals
* \[task-name]-auto-deals.csv: Deal CID updated based on \[task-name]-metadata.csv generated on next step.
* \[task-name]-auto-deals.json: Deal CID updated based on \[task-name]-metadata.json generated on next step. See [Offline Deal](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Offline-Deal)

**Note:**

* Logs are in directory ./logs
* To avoid program exit when you log out, you can run the program like this:

```
nohup ./swan-client auto -out-dir [output_files_dir] >> swan-client.log &
```
