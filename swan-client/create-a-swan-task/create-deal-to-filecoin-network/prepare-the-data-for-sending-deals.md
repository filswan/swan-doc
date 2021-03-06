# Prepare data for sending deals

### Create Car Files

🔔 The input dir and out dir should only be absolute one.

🔔 This step is necessary for tasks in all of the bid modes. You can choose one of the following 3 options.

#### Option1️⃣ By Lotus

🔔 This option will generate a car file for each file in source directory.

```
./swan-client car -input-dir [input_files_dir] -out-dir [car_files_output_dir]
```

**Command parameters used in this step:**

* \-input-dir(Required): The directory where the source files reside in.
* \-out-dir(optional): Car files and metadata files will be generated into this directory. When omitted, use `[sender].output_dir` in [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

**Configurations used in this step:**

* \[lotus].client\_api\_url, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[lotus].client\_access\_token, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].output\_dir, only used when -out-dir is omitted in command, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].generate\_md5, when it is true, then generate md5 for source files and car files, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

**Files generated after this step:**

* car.json: contains information for both source files and car files, see [Offline Deal](https://github.com/filswan/go-swan-client/tree/main#Offline-Deal)
* \[source-file-name].car: each source file has a related car file

#### Option2️⃣ By graphsplit API

🔔 This option can split a file under the source directory to one or more car file(s) in the output directory.

```
./swan-client gocar -input-dir [input_files_dir] -out-dir [car_files_output_dir]
```

**Command parameters used in this step:**

* \-input-dir(Required): The directory where the source files reside in.
* \-out-dir(optional): Car files and metadata files will be generated into this directory. When omitted, use `[sender].output_dir` in [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

**Configurations used in this step:**

* \[lotus].client\_api\_url, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[lotus].client\_access\_token, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].gocar\_file\_size\_limit, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].gocar\_folder\_based, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].output\_dir, only used when -out-dir is omitted in command, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].generate\_md5, when it is true, then generate md5 for source files and car files, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

**Files generated after this step:**

* manifest.csv: this is generated by `graphsplit api`
* car.json: contains information for both source files and car files, see [Offline Deal](https://github.com/filswan/go-swan-client/tree/main#Offline-Deal), generated from `manifest.csv`
* \[hash-value-of-file-part].car: if `gocar_folder_based=true`, the folder will have one or more car files, otherwize each a source file will have one or more related car file(s), according to its size and `[sender].gocar_file_size_limit`

**Note:**

* If source filesize is greater than `[sender].gocar_file_size_limit`, the source file information in the metadata files are for temporary source files, which are generated by `graphsplit api`, and after the car files are generated, those temporary source files will be deleted by `graphsplit api`. And in this condition, we do not create source file MD5 in the metadata files.

Credits should be given to filedrive-team. More information can be found in [https://github.com/filedrive-team/go-graphsplit](https://github.com/filedrive-team/go-graphsplit).

#### Option3️⃣ By Ipfs Web Api

🔔 This option will merge files under source directory to one car file in output directory using ipfs web api.

```
./swan-client ipfscar -input-dir [input_files_dir] -out-dir [car_file_output_dir]
```

**Command parameters used in this step:**

* \-input-dir(Required): The directory where the source files reside in.
* \-out-dir(optional): Car file and metadata files will be generated into this directory. When omitted, use `[sender].output_dir` in [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

**Configurations used in this step:**

* \[lotus].client\_api\_url, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[lotus].client\_access\_token, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].output\_dir, only used when -out-dir is omitted in command, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].generate\_md5, when it is true, then generate md5 for source files and car files, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[ipfs\_server].upload\_url\_prefix, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

**Files generated after this step:**

* car.json: contains information for car file, see [Offline Deal](https://github.com/filswan/go-swan-client/tree/main#Offline-Deal)
* \[car-file-cid].car: the source file(s) will be merged into this car file

#### Option4️⃣ By ipfs-car Command

🔔 ipfs-car command should be installed first using

```
sudo npm install -g ipfs-car
```

🔔 This option will merge files under source directory to one car file in output directory using ipfs-car command.

```
./swan-client ipfscmdcar -input-dir [input_files_dir] -out-dir [car_file_output_dir]
```

**Command parameters used in this step:**

* \-input-dir(Required): The directory where the source files reside in.
* \-out-dir(optional): Car file and metadata files will be generated into this directory. When omitted, use `[sender].output_dir` in [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

**Configurations used in this step:**

* \[lotus].client\_api\_url, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[lotus].client\_access\_token, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].output\_dir, only used when -out-dir is omitted in command, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)
* \[sender].generate\_md5, when it is true, then generate md5 for source files and car files, see [Configuration](https://github.com/filswan/go-swan-client/tree/main#Configuration)

**Files generated after this step:**

* car.json: contains information for car file, see [Offline Deal](https://github.com/filswan/go-swan-client/tree/main#Offline-Deal)
* \[source-files-dir-name].car: the source file(s) will be merged into this car file
