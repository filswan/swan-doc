---
description: How to create and delete bucket in Buckets
---

# Create and Delete Buckets

### Create Bucket

Buckets APIs allow users to create and delete buckets (At the current version of Buckets, only 1 bucket is allowed per user)

```python
api.create_bucket(<bucket_name>)
```

### Delete Bucket

To delete a bucket, the bucket's id is required. We can retrieve this id using the `get_bucket_id` function.

```python
bucket_id = api.get_bucket_id(<bucket_name>)
api.delete_bucket(bucket_id)
```
