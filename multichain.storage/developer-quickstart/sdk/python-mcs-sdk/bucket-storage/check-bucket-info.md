---
description: How to check bucket and file information
---

# Check Bucket Info

You can use Buckets APIs to check bucket and file information, including `name`, `id`, `session policy`, etc.

```python
print(bucket_api.get_buckets())
# folder name is optional parameter, 
# use when store file inside a folder within the bucket
print(bucket_api.get_file_list(<bucket_id>, <folder_name>))
print(bucket_api.get_full_file_list(<bucket_id>, <folder_name>))
```

