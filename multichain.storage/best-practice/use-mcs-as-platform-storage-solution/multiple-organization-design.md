---
description: For multiple organizations or a organization has more function unit.
---

# Multiple Organization Design

<figure><img src="../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

## Step-by-Step Tutorial

### Login to Multichain Storage

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Create Buckets for Organizations

Click "**Bucket Storage**" -> "**Create Bucket**", then enter your bucket name.

Use create multiple buckets for each organization or function.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-03-02 at 5.43.32 PM.png" alt=""><figcaption></figcaption></figure>

#### Create folders for each user

First, install mcs python SDK

```
pip install python-mcs-sdk
```

MCS is a bucket-based object storage, insider bucket, folder, sub-folders and file name is defined as the object key, file content is defined as object value.

e.g. If we have a function called OnchainStorage and a user wallet **0x165CD37b4C644C2921454429E7F9358d18A45e14.** Now we want to use this wallet as a folder name and upload a file called **flower.jpeg**

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

Then we can upload the user file to the bucket:

```python
mcs_file = upload_replace_file(file_path, "OchainStorage",os.path.join("0x165CD37b4C644C2921454429E7F9358d18A45e
```

You should see the following file stored in your multichain bucket.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-03-02 at 6.05.26 PM.png" alt=""><figcaption></figcaption></figure>

This process can be repeated with other organizations or functions for your application.

Put everything together:

```
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
    mcs_file = upload_replace_file(file_path, "OnchainStorage",
                                   os.path.join("0x165CD37b4C644C2921454429E7F9358d18A45e14", "apple.jpeg"))

```
