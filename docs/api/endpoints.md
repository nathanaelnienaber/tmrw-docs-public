# API Endpoints

## List All Resources
**GET** `/resources`

### Parameters
None.

### Example Response
```json
[
  {
    "id": 1,
    "name": "Resource 1",
    "type": "example"
  }
]
```

## Get Resource by ID
**GET** `/resources/{id}`

### Parameters
| Name | Type   | Description        |
|------|--------|--------------------|
| id   | String | Unique resource ID |

### Example Response
```json
{
  "id": 1,
  "name": "Resource 1",
  "type": "example"
}
```
