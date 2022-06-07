# Auto-bid Deal

### Option2️⃣ Auto-bid deal

* After a miner is allocated to a car file by Market Matcher, the client needs to send auto-bid deals using the information submitted to swan in step [Create A Task](https://github.com/filswan/go-swan-client/tree/main#Create-A-Task).
* This step is executed in infinite loop mode, it will send auto-bid deals contiuously when there are deals that can meet below conditions.

**Conditions:**

* `your tasks in swan`
* `task.bid_mode=1`
* `offline_deals.status=Assigned`

```
./swan-client auto -out-dir [output_files_dir]
```

**Command parameters used in this step:**

* \-out-dir(optional): Swan deal final metadata files will be generated to the given directory. When ommitted, use default: `[sender].output_dir`. See [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

**Configurations used in this step:**

* \[sender].wallet, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].output\_dir, only used when -out-dir is omitted in command, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[main].api\_url, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[main].api\_key, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[main].access\_token, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

**Files generated for each task after this step:**

* \[task-name]-auto-deals.json: Deal CID updated based on \[task-name]-metadata.json generated on next step. See [Offline Deal](https://github.com/filswan/go-swan-client/tree/main#Offline-Deal)

**Note:**

* Logs are in directory ./logs
* You can add `nohup` before `./swan-client` to ignore the HUP (hangup) signal and therefore avoid stop when you log out.
* You can add `>> swan-client.log` in the command to let all the logs output to `swan-client.log`.
* You can add `&` at the end of the command to let the program run in background.
* Such as:

```
nohup ./swan-client auto -out-dir [output_files_dir] >> swan-client.log &
```
