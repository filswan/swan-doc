---
description: Tutorial for accessing bucket through Python MCS SDK
---

# Bucket Storage

In a multichain storage system, a bucket is a logical container that stores folders or files. Each bucket has a unique name and can contain any number of folders and files. Folders are virtual containers that organize files and help manage data, and files are individual data objects that can be of any type or format. MCS Bucket files are referred to as objects.

This section describes how to use the python-MCS-SDK to perform common operations on the MCS bucket.

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
for i in bucket_client.list_buckets():
    print(i.to_json())
```

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)
# Return true if bucket created, else False
bucket_client.delete_bucket(bucket_name)
```

<pre class="language-python"><code class="lang-python">from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("&#x3C;API_KEY>", "&#x3C;ACCESS_TOKEN>", "&#x3C;CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)
<strong># Return None if MCS cannot find this bucket
</strong>print(bucket_client.get_bucket("&#x3C;BUCKET_NAME>","&#x3C;BUCKET_UID>").to_json())
</code></pre>

### Create an MCS Bucket

`create_bucket(bucket_name)`

Creates a bucket. Buckets under the same account cannot share the same name.

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)

bucket_client.create_bucket("<BUCKET_NAME>")
```

#### Parameters

* **bucket\_name**: The name of the bucket&#x20;

#### Return

Returns True if the bucket creation was successful

<pre class="language-python"><code class="lang-python"><strong>True
</strong></code></pre>

### Get Buckets

`list_buckets()`

List all the existing buckets for the MCS account.

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)

for i in bucket_client.list_buckets():
    print(i.to_json())
```

#### Return

Returns a list of Bucket Objects

```json
{
    "address": "0xA87...9b0",
    "bucket_name": "test-bucket",
    "bucket_uid": "8721a157-8233-4d08-bb11-1911e759c2bb",
    "created_at": "2023-01-04T17:52:04Z",
    "deleted_at": null,
    "file_number": 4,
    "is_active": true,
    "is_deleted": false,
    "is_free": true,
    "max_size": 34359738368,
    "size": 9988,
    "updated_at": "2023-01-04T17:52:04Z"
}
{
    "address": "0xA87...9b0",
    "bucket_name": "test-bucket2",
    "bucket_uid": "552f8339-4d01-4163-8e1e-34e4b1df22fe",
    "created_at": "2023-02-27T16:20:48Z",
    "deleted_at": null,
    "file_number": 0,
    "is_active": true,
    "is_deleted": false,
    "is_free": true,
    "max_size": 34359738368,
    "size": 0,
    "updated_at": "2023-02-27T16:20:48Z"
}
...
```

### Delete Bucket

`delete_bucket(bucket_name)`

Removes a bucket from your account.

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)

bucket_client.delete_bucket("<BUCKET_NAME>")
```

#### Parameters

* **bucket\_name**: The name of the bucket&#x20;

#### Return

Returns True if the deletion was successful

<pre class="language-python"><code class="lang-python"><strong>True
</strong></code></pre>

### Get Bucket information

`get_bucket(bucket_name)`

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)

print(bucket_client.get_bucket("<BUCKET_NAME>").to_json())
```

#### Parameters

* **bucket\_name**: The name of the bucket&#x20;

#### Return

Returns a Bucket Object

```json
{
    "address": "0xA87...9b0",
    "bucket_name": "test-bucket",
    "bucket_uid": "8721a157-8233-4d08-bb11-1911e759c2bb",
    "created_at": "2023-01-04T17:52:04Z",
    "deleted_at": null,
    "file_number": 4,
    "is_active": true,
    "is_deleted": false,
    "is_free": true,
    "max_size": 34359738368,
    "size": 9988,
    "updated_at": "2023-01-04T17:52:04Z"
}
```

### Create folder

`create_folder(bucket_name, folder_name, prefix='')`

The `create_folder` the method allows you to create a folder in the specified bucket. It accepts buckets name, folder names, and prefixes. The folder will be created in `bucket_name/prefix/folder_name`

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)

# If you want to place the folder directly in the root directory, you can leave the prefix field empty
bucket_client.create_folder("<BUCKET_NAME>","<FOLDER_NAME>","<PREFIX>")
```

#### Parameters

* **bucket\_name**: The name of the bucket&#x20;
* **folder\_name:** The name of the folder to create
* **prefix:** The prefix for the folder's object name

#### Return

Returns True if the folder creation was successful

```python
True
```

### Uploading file

`upload_file(bucket_name, object_name, file_path, replace=False)`

Uploads a file to a bucket. Use the `bucket_name` to select the bucket, and `object_name` to select the path and file name of the uploaded file. `file_path` is the local path of the file.

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)

# Object name is the destination path you want to upload to the bucket
# For example, if you want to upload the testfile.json file to path 111/222 in the TEST bucket, you would write: 
# bucket_client.upload_file("TEST", "111/222/testfile.json", "<FILE_PATH>")
bucket_client.upload_file("<BUCKET_NAME>", "<OBJECT_NAME>", "<FILE_PATH>")
```

#### Parameters

* **bucket\_name**: The name of the bucket&#x20;
* **object\_name:** The object name of the file ex. `'folder1/file.png'` will upload the file as `file.png` inside `bucket_name/folder1`
* **file\_path:** The local file path
* **replace:** File's of the same name cannot be uploaded. When replace is set to True, it will overwrite the previous file of the same name.

#### Return

Returns a File Object

```json
{
    "address": "0xA87...9b0",
    "bucket_uid": "8721a157-8233-4d08-bb11-1911e759c2bb",
    "created_at": "2023-02-08T18:35:33Z",
    "deleted_at": null,
    "filehash": "65a8e27d8879283831b664bd8b7f0ad4",
    "gateway": "https://fce2d84f11.calibration-swan-acl.filswan.com/",
    "id": 6153,
    "ipfs_url": "https://ipfs.multichain.storage/ipfs/Qm...",
    "is_deleted": false,
    "is_folder": false,
    "name": "file1.txt",
    "object_name": "file1.txt",
    "payloadCid": "Qm...",
    "pin_status": "Pinned",
    "prefix": "",
    "size": 13,
    "type": 2,
    "updated_at": "2023-02-08T18:35:33Z"
}
```

### Uploading MCS Folder

`upload_folder(self, bucket_name, object_name, folder_path)`

Uploads `folder_path` as a MCS folder under `bucket_name`/`object_name`

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)

bucket_client.upload_folder("<BUCKET_NAME>", "<OBJECT_NAME>", "<FOLDER_PATH>")
```

**Parameters**

* bucket\_name: The name of the bucket
* object\_name: The object name for the folder
* folder\_path: Local path of your folder

**Return**

Returns a list of File Objects

```json
[
  {
    "address": "0xA87...9b0",
    "bucket_uid": "8721a157-8233-4d08-bb11-1911e759c2bb",
    "created_at": "2023-02-08T18:35:33Z",
    "deleted_at": null,
    "filehash": "65a8e27d8879283831b664bd8b7f0ad4",
    "gateway": "https://fce2d84f11.calibration-swan-acl.filswan.com/",
    "id": 6153,
    "ipfs_url": "https://ipfs.multichain.storage/ipfs/Qm...",
    "is_deleted": false,
    "is_folder": false,
    "name": "file1.txt",
    "object_name": "file1.txt",
    "payloadCid": "Qm...",
    "pin_status": "Pinned",
    "prefix": "",
    "size": 13,
    "type": 2,
    "updated_at": "2023-02-08T18:35:33Z"
  },
  {
    "address": "0xA87...9b0",
    "bucket_uid": "8721a157-8233-4d08-bb11-1911e759c2bb",
    "created_at": "2023-02-08T18:35:33Z",
    "deleted_at": null,
    "filehash": "65a8e27d8879283831b664bd8b7f0ad4",
    "gateway": "https://fce2d84f11.calibration-swan-acl.filswan.com/",
    "id": 6153,
    "ipfs_url": "https://ipfs.multichain.storage/ipfs/Qm...",
    "is_deleted": false,
    "is_folder": false,
    "name": "file1.txt",
    "object_name": "file1.txt",
    "payloadCid": "Qm...",
    "pin_status": "Pinned",
    "prefix": "",
    "size": 13,
    "type": 2,
    "updated_at": "2023-02-08T18:35:33Z"
  },
...
]
```

### Upload IPFS Folder

`upload_ipfs_folder(self, bucket_name, object_name, folder_path)`

Uploads `folder_path` as an IPFS folder to MCS. This gives the folder its own CID, sharable to others.

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)

bucket_client.upload_ipfs_folder("<BUCKET_NAME>", "<OBJECT_NAME>", "<FOLDER_PATH>")
```

**Parameters**

* bucket\_name: The name of the bucket
* object\_name: The object name for the folder
* folder\_path: Local path of your folder

**Return**

Returns a File Object for your IPFS folder

```python
{
    "address": "0xA87...9b0",
    "bucket_uid": "8721a157-8233-4d08-bb11-1911e759c2bb",
    "created_at": "2023-02-08T18:35:33Z",
    "deleted_at": null,
    "filehash": "65a8e27d8879283831b664bd8b7f0ad4",
    "gateway": "https://fce2d84f11.calibration-swan-acl.filswan.com/",
    "id": 6153,
    "ipfs_url": "https://ipfs.multichain.storage/ipfs/Qm...",
    "is_deleted": false,
    "is_folder": false,
    "name": "file1.txt",
    "object_name": "ipfs-folder1",
    "payloadCid": "Qm...",
    "pin_status": "Pinned",
    "prefix": "",
    "size": 13,
    "type": 1,
    "updated_at": "2023-02-08T18:35:33Z"
}
```

### Downloading file

`download_file(bucket_name, object_name, local_filename)`

Downloads the file (located using `bucket_name`/`object_name` from IPFS and writes it to `local_filename`

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)

bucket_client.download_file("<BUCKET_NAME>", "<OBJECT_NAME>", "<LOCAL_FILENAME>")
```

#### Parameters

* **bucket\_name**: The name of the bucket&#x20;
* **object\_name:** The object name to download
* **local\_filename:** The download destination and filename

#### Return

Returns True if the file was downloaded successfully

```python
True
```

### Deleting file

`delete_file(bucket_name, object_name)`

Removes a file from a bucket

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)

bucket_client.delete_file("<BUCKET_NAME>", "<OBJECT_NAME>")
```

#### Parameters

* **bucket\_name**: The name of the bucket&#x20;
* **object\_name:** The object name to delete

#### Return

Returns True if the deletion was successful

```python
True
```

### Get file

`get_file(bucket_name, object_name)`

Get the file information of a file in one of your buckets

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)

print(bucket_client.get_file("<BUCKET_NAME>", "<OBJECT_NAME>").to_json())
```

#### Parameters

* **bucket\_name**: The name of the bucket&#x20;
* **object\_name:** The object name of the file

#### Return

Returns a File Object

```json
{
    "address": "0xA87...9b0",
    "bucket_uid": "8721a157-8233-4d08-bb11-1911e759c2bb",
    "created_at": "2023-02-08T18:35:33Z",
    "deleted_at": null,
    "filehash": "65a8e27d8879283831b664bd8b7f0ad4",
    "gateway": "https://fce2d84f11.calibration-swan-acl.filswan.com/",
    "id": 6153,
    "ipfs_url": "https://ipfs.multichain.storage/ipfs/Qm...",
    "is_deleted": false,
    "is_folder": false,
    "name": "file1.txt",
    "object_name": "file1.txt",
    "payloadCid": "Qm...",
    "pin_status": "Pinned",
    "prefix": "",
    "size": 13,
    "type": 2,
    "updated_at": "2023-02-08T18:35:33Z"
}
```

### Get file list

`list_files(bucket_name, prefix='', limit=10, offset=0)`

Get a list of file information from one of your buckets

```python
from swan_mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)

for i in api.list_files("<BUCKET_NAME>", '<PREFIX>', "<LIMIT>", '<OFFSET>'):
    print(i.to_json())
```

#### Return

Returns a list of File Objects

```json
[
  {
    "address": "0xA87...9b0",
    "bucket_uid": "8721a157-8233-4d08-bb11-1911e759c2bb",
    "created_at": "2023-02-08T18:35:33Z",
    "deleted_at": null,
    "filehash": "65a8e27d8879283831b664bd8b7f0ad4",
    "gateway": "https://fce2d84f11.calibration-swan-acl.filswan.com/",
    "id": 6153,
    "ipfs_url": "https://ipfs.multichain.storage/ipfs/Qm...",
    "is_deleted": false,
    "is_folder": false,
    "name": "file1.txt",
    "object_name": "file1.txt",
    "payloadCid": "Qm...",
    "pin_status": "Pinned",
    "prefix": "",
    "size": 13,
    "type": 2,
    "updated_at": "2023-02-08T18:35:33Z"
  },
  {
    "address": "0xA87...9b0",
    "bucket_uid": "8721a157-8233-4d08-bb11-1911e759c2bb",
    "created_at": "2023-02-08T18:35:33Z",
    "deleted_at": null,
    "filehash": "65a8e27d8879283831b664bd8b7f0ad4",
    "gateway": "https://fce2d84f11.calibration-swan-acl.filswan.com/",
    "id": 6153,
    "ipfs_url": "https://ipfs.multichain.storage/ipfs/Qm...",
    "is_deleted": false,
    "is_folder": false,
    "name": "file1.txt",
    "object_name": "file1.txt",
    "payloadCid": "Qm...",
    "pin_status": "Pinned",
    "prefix": "",
    "size": 13,
    "type": 2,
    "updated_at": "2023-02-08T18:35:33Z"
  },
...
]
```
