---
description: Auto send auto-bid mode tasks with deals to auto-bid mode storage provider
---

# Public and Manual-Bid Task

### Option3️⃣ Public and Manual-Bid Task

* **Conditions:** `[sender].public_deal=true` and `[sender].bid_mode=0`, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)

```
./swan-client task -input-dir [car_files_dir] -out-dir [output_files_dir] -dataset [curated_dataset] -description [description]
```

**Command parameters used in this step:**

* \-input-dir(Required): Input directory where the generated car files and metadata files reside in.
* \-out-dir(optional): Metadata files and swan task files will be generated to this directory. When omitted, use the default `[send].output_dir`, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \-dataset(optional): The curated dataset from which the car files are generated
* \-description(optional): Details to better describe the data and confine the task or anything the storage provider needs to be informed.

**Configurations used in this step:**

* \[sender].public\_deal, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[sender].bid\_mode, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[sender].verified\_deal, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[sender].offline\_mode, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[sender].fast\_retrieval, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[sender].max\_price, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[sender].start\_epoch\_hours, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[sender].expire\_days, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[sender].generate\_md5, when it is true and there is no md5 in car.json, then generate md5 for source files and car files, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[sender].duration, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[sender].output\_dir, only used when -out-dir is omitted in command, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[main].storage\_server\_type, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[main].api\_url, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[main].api\_key, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[main].access\_token, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[web\_server].download\_url\_prefix, used only when `[main].storage_server_type="web server"`, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)

**Files generated after this step:**

* \[task-name].csv: A CSV generated for posting a task and its offline deals on Swan platform or transferring to storage providers directly for offline import
* \[task-name]-metadata.csv: Contains more contents used for review. Uuid will be updated based upon car.csv generated in last step.
* \[task-name]-metadata.json: Contains more content for creating a proposal in the next step. Uuid will be updated based on car.json generated in the last step. See [Offline Deal](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Offline-Deal)
