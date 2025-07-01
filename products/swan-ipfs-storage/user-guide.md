# Swan IPFS Storage User Guide

This guide explains how to use Swan IPFS Storage for decentralized file storage and retrieval.

## Uploading Files

### Using the Web UI
1. Go to the [Swan IPFS Storage Portal](https://storage.swancloud.ai/)
2. Log in or create an account
3. Click "Upload" and select your files
4. After upload, you'll receive an IPFS CID (Content Identifier)

### Using the API
- **POST** `/api/storage/upload`
- **Headers:**
  - `Authorization: Bearer <your_api_key>`
- **Body:** Multipart form with file(s)
- **Response:**
  ```json
  {
    "cid": "<ipfs_cid>",
    "status": "success"
  }
  ```

## Retrieving Files

- Use the IPFS CID to retrieve files:
  - Via the portal: Search or browse by CID
  - Via API: **GET** `/api/storage/file/<cid>`
  - Via public IPFS gateways: `https://ipfs.io/ipfs/<cid>`

## Managing Files

- List your files: **GET** `/api/storage/list`
- Delete a file: **DELETE** `/api/storage/file/<cid>`

## Best Practices

- Keep your API key secure
- Use descriptive filenames and metadata
- Regularly back up important CIDs

See the [API Reference](api.md) for more details. 