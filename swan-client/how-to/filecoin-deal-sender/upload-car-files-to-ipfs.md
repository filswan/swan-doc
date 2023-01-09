# Upload CAR Files to IPFS

:bell:- `[ipfs_server].download_url_prefix` and `[ipfs_server].upload_url_prefix` are required to upload CAR files to IPFS server.

```shell
./swan-client upload -input-dir [input_file_dir]

OPTIONS:
   --input-dir value, -i value  directory where source files are in.

```

**Files updated after this step:**

* `car.json`: the `CarFileUrl` of CAR files will be updated
* `car.csv`: the `CarFileUrl` of CAR files will be updated
