# Swan IPFS Storage API Reference

Interact with Swan IPFS Storage using these RESTful API endpoints.

## Authentication

All endpoints require an API key in the `Authorization` header:

```
Authorization: Bearer <your_api_key>
```

## Endpoints

### 1. Upload File
- **POST** `/api/storage/upload`
- **Description:** Upload one or more files to IPFS storage.
- **Body:** Multipart form data with file(s)
- **Response:**
  ```json
  {
    "cid": "<ipfs_cid>",
    "status": "success"
  }
  ```

### 2. Retrieve File
- **GET** `/api/storage/file/<cid>`
- **Description:** Download a file by its IPFS CID.
- **Response:** File content

### 3. List Files
- **GET** `/api/storage/list`
- **Description:** List all files uploaded by the authenticated user.
- **Response:**
  ```json
  [
    {
      "cid": "<ipfs_cid>",
      "filename": "string",
      "uploaded_at": "timestamp"
    }
  ]
  ```

### 4. Delete File
- **DELETE** `/api/storage/file/<cid>`
- **Description:** Delete a file by its CID.
- **Response:**
  ```json
  {
    "status": "deleted"
  }
  ```

## Error Handling

- Errors are returned as JSON with an `error` field and HTTP status code. 