# Swan Provider API Reference

Swan Providers interact with the network and Swan Cloud platform via a RESTful API. Below are the main endpoints and usage patterns.

## Authentication

All endpoints require an API key. Include it in the `Authorization` header:

```
Authorization: Bearer <your_api_key>
```

## Endpoints

### 1. Register Provider
- **POST** `/api/providers/register`
- **Description:** Register a new provider node with the network.
- **Body:**
  ```json
  {
    "name": "string",
    "contact": "string",
    "resources": {
      "cpu": "number",
      "ram": "number",
      "storage": "number"
    }
  }
  ```
- **Response:** Provider ID and registration status.

### 2. Report Status
- **POST** `/api/providers/status`
- **Description:** Report current resource usage and node health.
- **Body:**
  ```json
  {
    "provider_id": "string",
    "cpu_usage": "number",
    "ram_usage": "number",
    "storage_usage": "number",
    "status": "online|offline|maintenance"
  }
  ```
- **Response:** Status confirmation.

### 3. Update Resources
- **PUT** `/api/providers/resources`
- **Description:** Update available resources for your provider node.
- **Body:**
  ```json
  {
    "provider_id": "string",
    "cpu": "number",
    "ram": "number",
    "storage": "number"
  }
  ```
- **Response:** Update confirmation.

## Error Handling

- All errors are returned as JSON with an `error` field and HTTP status code.

## More

- See the [Developer API Reference](../../developer/api-reference.md) for advanced integration. 