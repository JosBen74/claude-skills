# API Design Skill

Design consistent, well-documented REST APIs following industry best practices.

## Trigger

Activated when user asks for:
- API endpoints
- REST API design
- Backend routes
- API documentation
- Request/response schemas

## Core Principles

### 1. Resource-Oriented Design

APIs are organized around **resources** (nouns), not actions (verbs).

```
GOOD:
  GET    /users
  POST   /users
  GET    /users/:id

BAD:
  GET    /getUsers
  POST   /createUser
  GET    /fetchUserById
```

### 2. URL Structure

```
https://api.example.com/v1/resources/:id/sub-resources

Components:
- Protocol: https (always)
- Subdomain: api.example.com (or /api prefix)
- Version: /v1
- Resource: plural nouns (users, products, orders)
- Identifier: :id (UUID or slug)
- Sub-resource: nested resources
```

**Examples**:
```
GET  /v1/users                    # List users
GET  /v1/users/123                # Get user
GET  /v1/users/123/orders         # User's orders
GET  /v1/users/123/orders/456     # Specific order
POST /v1/users/123/orders         # Create order for user
```

## HTTP Methods

| Method | Usage | Idempotent | Request Body | Response |
|--------|-------|------------|--------------|----------|
| GET | Retrieve resource(s) | Yes | No | Resource(s) |
| POST | Create resource | No | Yes | Created resource |
| PUT | Replace resource entirely | Yes | Yes | Updated resource |
| PATCH | Partial update | Yes | Yes | Updated resource |
| DELETE | Remove resource | Yes | No | Empty (204) |

### Method Selection Guide

```
Need to...                          Use...
─────────────────────────────────────────────
Fetch data                          GET
Create new resource                 POST
Update (full replacement)           PUT
Update (partial, specific fields)   PATCH
Remove resource                     DELETE
Check if resource exists            HEAD
Get allowed methods                 OPTIONS
```

## HTTP Status Codes

### Success (2xx)

| Code | Meaning | When to use |
|------|---------|-------------|
| 200 | OK | GET, PUT, PATCH success |
| 201 | Created | POST success (include Location header) |
| 204 | No Content | DELETE success, PUT/PATCH with no body |

### Client Errors (4xx)

| Code | Meaning | When to use |
|------|---------|-------------|
| 400 | Bad Request | Validation error, malformed JSON |
| 401 | Unauthorized | Missing or invalid authentication |
| 403 | Forbidden | Authenticated but not allowed |
| 404 | Not Found | Resource doesn't exist |
| 409 | Conflict | Duplicate entry, state conflict |
| 422 | Unprocessable Entity | Semantic validation error |
| 429 | Too Many Requests | Rate limit exceeded |

### Server Errors (5xx)

| Code | Meaning | When to use |
|------|---------|-------------|
| 500 | Internal Server Error | Unexpected server error |
| 502 | Bad Gateway | Upstream service failed |
| 503 | Service Unavailable | Maintenance, overload |

## Response Format

### Standard Success Response

```json
{
  "data": {
    "id": "usr_abc123",
    "type": "user",
    "attributes": {
      "email": "user@example.com",
      "name": "John Doe",
      "created_at": "2024-01-15T10:30:00Z"
    }
  }
}
```

### Collection Response (with pagination)

```json
{
  "data": [
    { "id": "usr_abc123", "type": "user", "attributes": {...} },
    { "id": "usr_def456", "type": "user", "attributes": {...} }
  ],
  "meta": {
    "total": 150,
    "page": 1,
    "per_page": 20,
    "total_pages": 8
  },
  "links": {
    "self": "/v1/users?page=1",
    "next": "/v1/users?page=2",
    "last": "/v1/users?page=8"
  }
}
```

### Error Response

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "The request contains invalid data",
    "details": [
      {
        "field": "email",
        "code": "INVALID_FORMAT",
        "message": "Must be a valid email address"
      },
      {
        "field": "age",
        "code": "OUT_OF_RANGE",
        "message": "Must be between 18 and 120"
      }
    ],
    "request_id": "req_xyz789"
  }
}
```

### Error Codes (standardized)

```
Authentication:
  AUTH_REQUIRED         - No token provided
  AUTH_INVALID          - Token invalid or expired
  AUTH_FORBIDDEN        - Not allowed to access resource

Validation:
  VALIDATION_ERROR      - Generic validation failure
  INVALID_FORMAT        - Wrong format (email, date, etc.)
  REQUIRED_FIELD        - Missing required field
  OUT_OF_RANGE          - Value outside allowed range
  DUPLICATE_ENTRY       - Unique constraint violation

Resources:
  NOT_FOUND             - Resource doesn't exist
  ALREADY_EXISTS        - Cannot create duplicate
  CONFLICT              - State conflict

Rate Limiting:
  RATE_LIMITED          - Too many requests
```

## Pagination

### Query Parameters

```
GET /v1/users?page=2&per_page=20

Parameters:
  page      - Page number (1-indexed)
  per_page  - Items per page (default: 20, max: 100)

OR cursor-based:
  cursor    - Opaque cursor for next page
  limit     - Items to return
```

### Response Headers

```
X-Total-Count: 150
X-Page: 2
X-Per-Page: 20
X-Total-Pages: 8
Link: <...?page=1>; rel="first", <...?page=3>; rel="next"
```

## Filtering & Sorting

### Filtering

```
GET /v1/users?filter[status]=active
GET /v1/users?filter[role]=admin,editor
GET /v1/users?filter[created_at][gte]=2024-01-01
GET /v1/products?filter[price][lte]=100

Operators:
  eq    - Equal (default)
  ne    - Not equal
  gt    - Greater than
  gte   - Greater than or equal
  lt    - Less than
  lte   - Less than or equal
  in    - In array
  like  - Contains (string)
```

### Sorting

```
GET /v1/users?sort=created_at        # Ascending
GET /v1/users?sort=-created_at       # Descending (prefix -)
GET /v1/users?sort=-created_at,name  # Multiple fields
```

### Field Selection

```
GET /v1/users?fields=id,name,email
GET /v1/users?fields[users]=id,name&fields[orders]=id,total
```

## Authentication

### Bearer Token (JWT)

```
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...

Response if invalid:
  401 Unauthorized
  {
    "error": {
      "code": "AUTH_INVALID",
      "message": "Token is expired or invalid"
    }
  }
```

### API Key

```
X-API-Key: sk_live_abc123...

OR in query (less secure):
GET /v1/users?api_key=sk_live_abc123
```

## Rate Limiting

### Response Headers

```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 998
X-RateLimit-Reset: 1704067200
Retry-After: 60
```

### 429 Response

```json
{
  "error": {
    "code": "RATE_LIMITED",
    "message": "Too many requests",
    "retry_after": 60
  }
}
```

## Versioning

### URL Path (recommended)

```
/v1/users
/v2/users
```

### Header-based

```
Accept: application/vnd.api+json; version=1
API-Version: 2024-01-15
```

## Request Validation

### Required Headers

```
Content-Type: application/json
Accept: application/json
Authorization: Bearer <token>
```

### Common Validations

```yaml
email:
  format: email
  max_length: 255

password:
  min_length: 8
  pattern: "must contain uppercase, lowercase, number"

id:
  format: uuid | prefixed (usr_, ord_)

date:
  format: ISO 8601 (2024-01-15T10:30:00Z)

pagination:
  page: integer, min 1
  per_page: integer, min 1, max 100
```

## Documentation (OpenAPI 3.0)

Always generate OpenAPI spec for APIs:

```yaml
openapi: 3.0.3
info:
  title: My API
  version: 1.0.0
  description: API description

servers:
  - url: https://api.example.com/v1

paths:
  /users:
    get:
      summary: List users
      tags: [Users]
      parameters:
        - $ref: '#/components/parameters/PageParam'
        - $ref: '#/components/parameters/PerPageParam'
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UserList'

components:
  schemas:
    User:
      type: object
      properties:
        id:
          type: string
          example: usr_abc123
        email:
          type: string
          format: email
        name:
          type: string
        created_at:
          type: string
          format: date-time

  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
```

## Constraints / NEVER

- NEVER use verbs in URLs (`/getUsers`, `/createOrder`)
- NEVER return 200 for errors (use proper status codes)
- NEVER expose internal IDs (use UUIDs or prefixed IDs)
- NEVER return stack traces in production errors
- NEVER accept GET requests with bodies
- NEVER use plural for singleton resources (`/me`, not `/mes`)
- NEVER mix snake_case and camelCase (pick one, stick to it)
- NEVER paginate without total count metadata

## Preferences

- Prefer snake_case for JSON fields
- Prefer UUIDs or prefixed IDs (`usr_`, `ord_`) over integers
- Prefer ISO 8601 for dates (`2024-01-15T10:30:00Z`)
- Prefer explicit `null` over omitting fields
- Prefer `filter[field]=value` over `field=value` for filtering
- Prefer cursor pagination for large datasets
- Prefer descriptive error codes over numeric codes

## Output Format

When generating APIs, always include:

1. **Endpoint list** with methods and descriptions
2. **Request/Response examples** for each endpoint
3. **Error responses** for common failure cases
4. **Authentication requirements**
5. **OpenAPI spec** (YAML) if requested
