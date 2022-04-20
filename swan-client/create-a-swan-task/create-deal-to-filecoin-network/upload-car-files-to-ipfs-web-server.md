# Upload Car files to IPFS/web server

### Upload Car Files

🔔 It is required to upload car files to the file server, either to a web server or to an IPFS server.

#### Option1️⃣ To a web-server manually

```
no swan-client subcommand should be executed
```

**Configurations used in this step:**

* \[main].storage\_server\_type, it should be set to `web server`, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)

#### Option2️⃣ To a local IPFS server

```
./swan-client upload -input-dir [input_file_dir]
```

**Command parameters used in this step:**

* \-input-dir(Required): The directory where the car files and metadata files reside in. Metadata files will be used and updated here after the car files are uploaded.

**Configurations used in this step:**

* \[main].storage\_server\_type, it should be set to `ipfs server`. See [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[ipfs\_server].download\_url\_prefix, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[ipfs\_server].upload\_url, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)
* \[sender].output\_dir, only used when -out-dir is omitted in command, see [Configuration](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Configuration)

**Files updated after this step:**

* car.csv: car file URL will be updated on the original one
* car.json: car file URL will be updated on the original one, see [Offline Deal](https://github.com/filswan/go-swan-client/tree/release-v0.1.0-rc1#Offline-Deal)
