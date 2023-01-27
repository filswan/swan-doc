---
description: CURD Bucket's files
---

# For file operations

### Uploading file

The python-MCS-SDK provides a pair of methods to upload a file to an MCS bucket.

The `upload_file` method accepts a file name, a bucket name, and an object name. The method handles large files by splitting them into smaller chunks and uploading each chunk in parallel.

```python
from mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)
# Object name is the destination path you want to upload to the bucket
# For example, if you want to upload the testfile.json file to path 111/222 in the TEST bucket, you would write: 
# bucket_client.upload_file("TEST", "111/222/testfile.json", "<FILE_PATH>")
bucket_client.upload_file("<BUCKET_NAME>", "<OBJECT_NAME>", "<FILE_PATH>")
```

### Downloading file

The methods provided by the python-MCS-SDK to download files are similar to those provided to upload files.

The `download_file` method accepts the names of the bucket and object to download and the filename to save the file to.

```python
from mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)
# Object name is the destination path you want to upload to the bucket
# For example, if you want to upload the testfile.json file to path 111/222 in the TEST bucket, you would write: 
# bucket_client.upload_file("TEST", "111/222/testfile.json", "<FILE_PATH>")
bucket_client.download_file("<BUCKET_NAME>", "<OBJECT_NAME>","<LOCAL_FILENAME>")
```

### Deleting file

The `delete_file` method accepts the names of the bucket and object to delete.

```python
from mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)
bucket_client.delete_file("<BUCKET_NAME>", "<OBJECT_NAME>")
```

### Get file

The methods provided by the python-MCS-SDK to delete files are similar to those provided to delete files.

The `get_file` method accepts the names of the bucket and object to get information.

```python
from mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)
print(bucket_client.get_file("<BUCKET_NAME>", "<OBJECT_NAME>").to_json())
```

### Get file list

The `get_file_list` method accepts four parameters: name of the bucket, prefix, and limit and offset for paging queries

```python
from mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)
for i in api.list_files("<BUCKET_NAME>", '<PREFIX>', "<LIMIT>", '<OFFSET>'):
    print(i.to_json())
```

### Create folder

The `create_folder` method allows you to create a folder in the specified bucket. It accepts buckets name, folder name, and prefix.

```python
from mcs import APIClient, BucketAPI
mcs_api = APIClient("<API_KEY>", "<ACCESS_TOKEN>", "<CHAIN_NAME>")
bucket_client = BucketAPI(mcs_api)
# If you want to place the folder directly in the root directory, you can leave the prefix field empty
bucket_client.create_folder("<BUCKET_NAME>","<FOLDER_NAME>","<PREFIX>")
```
