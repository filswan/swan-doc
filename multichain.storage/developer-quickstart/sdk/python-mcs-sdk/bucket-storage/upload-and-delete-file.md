---
description: Upload and delete file from Buckets
---

# Upload and Delete File

### Upload File

Uploading file to Buckets is similar to MCS. However, Buckets does not allow 2 files with the same name within 1 bucket.\
Therefore, you might want to use different file names when uploading the same file multiple times to a bucket.

<pre class="language-python"><code class="lang-python"><strong>bucket_api.upload_to_bucket(&#x3C;bucket_id>, &#x3C;file_path>)
</strong></code></pre>

{% hint style="info" %}
Use 'folder1/folder2' when there is multiple layers of folders.
{% endhint %}

### Delete File

Deleting a file from a bucket with bucket name and file id.

<pre class="language-python"><code class="lang-python"><strong># folder name is optional only use when file stored within folder 
</strong><strong>file_id = get_file_id(&#x3C;bucket_name>, &#x3C;file_name>, &#x3C;folder_name>):
</strong>bucket_api.delete_from_bucket(file_id)
</code></pre>

### Upload Folder

You can upload a folder of files to the designated bucket.

```python
# use the absolute path of the folder or relative path to the current directory
bucket_api.upload_folder(<bucket_id>, <folder_path>)
```

### Download File

To download files stored in a bucket.

```python
bucket_api.download_file(<bucket_id>, <file_name>, <folder_name>)
```
