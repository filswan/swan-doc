---
description: A simplified solution for applications only have platform storage space
---

# Single Organization Design

<figure><img src="../../../.gitbook/assets/image (4) (3).png" alt=""><figcaption></figcaption></figure>

## Step-by-Step Tutorial

### Login to Multichain Storage

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Create Platform bucket

Click "**Bucket Storage**" -> "**Create Bucket**", enter your bucket name.eg, **mcs\_1**

If the creation success, the bucket will be shown as below:

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### Create folder for each user

First install mcs python SDK

```
pip install python-mcs-sdk
```

MCS is a bucket based object storage, insider bucket, folder, sub-folders and file name is defined as object key,file content is defined as object value.

e.g if we have a user wallet is **0x165CD37b4C644C2921454429E7F9358d18A45e14**,  we want use this wallet as folder name and upload a file called **apple.jpeg**

```python
def upload_replace_file(file_path, bucket_name, dest_file_path):
    :param bucket_name: the bucket name user want to upload
    :param dest_file_path: the destination of the file you want to store exclude the bucket name
    :return: File Object
    """
    mcs_api = APIClient(api_key, access_token,network)
    bucket_client = BucketAPI(mcs_api)
    # check if file exist
    file_data = bucket_client.get_file(bucket_name, dest_file_path)
    if file_data:
        print("File exist,replace file: %s" % file_path)
        bucket_client.delete_file(bucket_name, dest_file_path)
    file_data = bucket_client.upload_file(bucket_name, dest_file_path, file_path)
    return file_data
```

Then we can upload user file to the bucket:

```python
mcs_file = upload_replace_file(file_path, "mcs_1",os.path.join("0x165CD37b4C644C2921454429E7F9358d18A45e14", "apple.jpeg"))
```

You should see the following file stored in your multichain bucket.

<figure><img src="../../../.gitbook/assets/image (1) (5).png" alt=""><figcaption></figcaption></figure>

Put everything together:

{% embed url="https://github.com/filswan/python-mcs-sdk/tree/main/sample/single_organization_design" %}

```python
import os

from mcs import APIClient, BucketAPI


def upload_replace_file(file_path, bucket_name, dest_file_path):
    """
    Upload a file by file path, bucket name and the target path
    :param file_path: the source file path
    :param bucket_name: the bucket name user want to upload
    :param dest_file_path: the destination of the file you want to store exclude the bucket name
    :return: File Object
    """
    mcs_api = APIClient(api_key, access_token,network)
    bucket_client = BucketAPI(mcs_api)
    # check if file exist
    file_data = bucket_client.get_file(bucket_name, dest_file_path)
    if file_data:
        print("File exist,replace file: %s" % file_path)
        bucket_client.delete_file(bucket_name, dest_file_path)
    file_data = bucket_client.upload_file(bucket_name, dest_file_path, file_path)
    return file_data


if __name__ == '__main__':
    api_key = "XXXX"
    access_token = "xxxxxxx"
    network = "polygon.mainnet"
    file_path = 'data/apple.jpeg'
    # file_path is the path relative to the current file
    # object_name is your target path
    mcs_file = upload_replace_file(file_path, "mcs_1",
                                   os.path.join("0x165CD37b4C644C2921454429E7F9358d18A45e14", "apple.jpeg"))

```
