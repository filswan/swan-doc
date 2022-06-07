# Upload Car files to IPFS/web server

### Upload Car Files

🔔 It is required to upload car files to file server(s), either to web server or to ipfs server.

#### Option1️⃣ To a web-server manually

```
no swan-client subcommand should be executed
```

**Configurations used in this step:**

* \[main].storage\_server\_type, it should be set to `web server`, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

#### Option2️⃣ To a local IPFS server

```
./swan-client upload -input-dir [input_file_dir]
```

**Command parameters used in this step:**

* \-input-dir(Required): The directory where the car files and metadata files reside in. Metadata files will be used and updated here after car files uploaded.

**Configurations used in this step:**

* \[main].storage\_server\_type, it should be set to `ipfs server`. See [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[ipfs\_server].download\_url\_prefix, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[ipfs\_server].upload\_url\_prefix, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].output\_dir, only used when -out-dir is omitted in command, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

**Files updated after this step:**

* car.json: car file url will be updated on the original one, see [Offline Deal](https://github.com/filswan/go-swan-client/tree/main#Offline-Deal)
