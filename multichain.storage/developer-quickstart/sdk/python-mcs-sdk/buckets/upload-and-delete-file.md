---
description: Upload and delete file from Buckets
---

# Upload and Delete File

### Upload File

Uploading file to Buckets is similar to MCS. However, Buckets does not allow 2 files with the same name within 1 bucket.\
Therefore, you might want to use different file names when uploading the same file multiple times to a bucket.

```python
api.upload_to_bucket(<bucket_name>, <file_name>, <file_path>)
```

### Delete File

Deleting a file from a bucket with bucket name and file id.

```python
file_id = get_file_id(<bucket_name>, <file_name>):
api.delete_from_bucket(file_id)
```
