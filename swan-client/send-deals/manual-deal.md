# Manual Deal

### Option1️⃣ Manual deal

**Conditions:**

* `task can be found by uuid in JSON file from swan platform`
* `task.bid_mode=0`

```
./swan-client deal -json [path]/[task-name]-metadata.json -out-dir [output_files_dir] -miner [storage_provider_ids]
```

**Command parameters used in this step:**

* \-json(Required): Full file path to the metadata JSON file, see [Offline Deal](https://github.com/filswan/go-swan-client/tree/main#Offline-Deal)
* \-out-dir(optional): Swan deal final metadata files will be generated to the given directory. When ommitted, use default: `[sender].output_dir`. See [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \-miner(Required): Storage provider Ids you want to send car files to, miners separated by comma if there are more than one, e.g `f01276` or `t03354,f01276`

**Configurations used in this step:**

* \[sender].wallet, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].verified\_deal, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].fast\_retrieval, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].start\_epoch\_hours, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].skip\_confirmation, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].max\_price, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].duration, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].output\_dir, only used when -out-dir is omitted in command, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[main].api\_url, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[main].api\_key, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[main].access\_token, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

**Files generated after this step:**

* \[task-name]-deals.json: Deal CID updated based on \[task-name]-metadata.json generated on previous step, see [Offline Deal](https://github.com/filswan/go-swan-client/tree/main#Offline-Deal)
