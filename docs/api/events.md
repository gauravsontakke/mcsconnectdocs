# Events API

## Get all events
`GET /api/events`

### Query Parameters
- `page` (number, optional, default: 1) - Page number for pagination
- `page_size` (number, optional, default: 10) - Number of items per page
- `sort_by` (string, optional) - Field to sort by (e.g., 'start_date', 'title')
- `sort_order` (string, optional) - Sort order ('asc' or 'desc')
- `category` (string, optional) - Filter by category

### Response
```json
[
  {
    "id": 201,
    "title": "Tech Conference",
    "description": "A gathering of tech minds.",
    "category": "Technology",
    "start_date": "2025-07-01",
    "end_date": "2025-07-02",
    "location": "Mumbai",
    "icon": "event-icon.png"
  }
]
```

## Get event details
`GET /api/events/{id}`

### Path Parameters
- `id` (required) - ID of the event

### Response
```json
{
  "id": 201,
  "title": "Tech Conference",
  "description": "A gathering of tech minds.",
  "category": "Technology",
  "start_date": "2025-07-01",
  "end_date": "2025-07-02",
  "location": "Mumbai",
  "icon": "event-icon.png",
  "registration_required": true,
  "registered_users_count": 120
}
```

## Create new event (Admin)
`POST /api/events`

### Headers
```
Authorization: Bearer <token>
Content-Type: application/json
```

### Request Body
```json
{
  "title": "Tech Conference",
  "description": "Event details",
  "category": "Technology",
  "start_date": "2025-07-01",
  "end_date": "2025-07-02",
  "location": "Mumbai",
  "icon": "event-icon.png"
}
```

### Response
```json
{
  "id": 201,
  "message": "Event created successfully"
}
```

## Update event (Admin)
`PUT /api/events/{id}`

### Headers
```
Authorization: Bearer <token>
Content-Type: application/json
```

### Path Parameters
- `id` (required) - ID of the event to update

### Request Body
```json
{
  "title": "Updated Tech Conference",
  "description": "Updated event details",
  "category": "Technology",
  "start_date": "2025-07-01",
  "end_date": "2025-07-03",
  "location": "Mumbai Convention Center",
  "icon": "updated-icon.png"
}
```

### Response
```json
{
  "message": "Event updated successfully"
}
```

## Delete event (Admin)
`DELETE /api/events/{id}`

### Headers
```
Authorization: Bearer <token>
```

### Path Parameters
- `id` (required) - ID of the event to delete

### Response
```json
{
  "message": "Event deleted successfully"
}
```

## Register for event
`POST /api/events/{id}/register`

### Headers
```
Authorization: Bearer <token>
Content-Type: application/json
```

### Path Parameters
- `id` (required) - ID of the event to register for

### Request Body
```json
{
  "username": "john_doe",
  "email": "john@example.com",
  "contact": "9876543210"
}
```

### Response
```json
{
  "message": "Registered successfully"
}
```

## Get event categories
`GET /api/events/categories`

### Response
```json
[
  {
    "id": 1,
    "name": "Technology",
    "description": "All about tech events",
    "icon": "tech-icon.png"
  }
]
```
- `end_date`
- `description`
- `category`