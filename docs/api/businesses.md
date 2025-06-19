# Business Directory API

## Get all businesses
`GET /api/businesses`

### Query Parameters
- `page` (number, optional, default: 1) - Page number
- `page_size` (number, optional, default: 10) - Items per page
- `category` (string, optional) - Filter by category ID
- `location` (string, optional) - Filter by location
- `search` (string, optional) - Search term for business name or description
- `sort_by` (string, optional) - Field to sort by (e.g., 'name', 'rating')
- `sort_order` (string, optional) - Sort order ('asc' or 'desc')

### Response
```json
{
  "businesses": [
    {
      "id": 1,
      "name": "Spice Bazaar",
      "description": "Authentic Indian restaurant",
      "category_id": 3,
      "address": "123 Main St, Mumbai",
      "contact_phone": "+919876543210",
      "contact_email": "info@spicebazaar.com",
      "website": "https://spicebazaar.com",
      "rating": 4.5,
      "review_count": 42,
      "logo": "logo1.jpg",
      "images": ["img1.jpg", "img2.jpg"],
      "is_verified": true,
      "created_at": "2024-01-15T10:30:00Z"
    }
  ],
  "pagination": {
    "total_items": 1,
    "total_pages": 1,
    "current_page": 1,
    "page_size": 10
  }
}
```

## Get business details
`GET /api/businesses/{id}`

### Path Parameters
- `id` (required) - ID of the business

### Response
```json
{
  "id": 1,
  "name": "Spice Bazaar",
  "description": "Authentic Indian restaurant serving traditional dishes from different regions of India.",
  "category": {
    "id": 3,
    "name": "Restaurant",
    "icon": "restaurant.png"
  },
  "owner_id": 123,
  "address": "123 Main St, Mumbai, Maharashtra 400001",
  "location": {
    "lat": 19.0760,
    "lng": 72.8777
  },
  "contact_phone": "+919876543210",
  "contact_email": "info@spicebazaar.com",
  "website": "https://spicebazaar.com",
  "opening_hours": [
    {"day": "monday", "open": "11:00", "close": "23:00"},
    {"day": "tuesday", "open": "11:00", "close": "23:00"},
    {"day": "sunday", "open": "12:00", "close": "22:00"}
  ],
  "rating": 4.5,
  "review_count": 42,
  "logo": "logo1.jpg",
  "images": ["img1.jpg", "img2.jpg"],
  "social_media": {
    "facebook": "spicebazaar",
    "instagram": "spicebazaar_official"
  },
  "is_verified": true,
  "created_at": "2024-01-15T10:30:00Z",
  "updated_at": "2024-05-20T15:45:00Z"
}
```

## Register new business
`POST /api/businesses`

### Headers
```
Authorization: Bearer <token>
Content-Type: multipart/form-data
```

### Request Body (form-data)
- `name` (string, required) - Business name
- `description` (string, required) - Business description
- `category_id` (number, required) - Business category ID
- `address` (string, required) - Full address
- `contact_phone` (string, required) - Contact number
- `contact_email` (string, required) - Contact email
- `website` (string, optional) - Business website
- `logo` (file, optional) - Business logo
- `images` (file[], optional) - Business images (max 5)
- `opening_hours` (JSON string, optional) - Opening hours in format: [{"day": "monday", "open": "09:00", "close": "18:00"}, ...]

### Response
```json
{
  "id": 1,
  "message": "Business registered successfully",
  "verification_required": true
}
```

## Update business
`PUT /api/businesses/{id}`

### Headers
```
Authorization: Bearer <token>
Content-Type: application/json
```

### Path Parameters
- `id` (required) - ID of the business to update

### Request Body
```json
{
  "name": "Spice Bazaar - Fine Dining",
  "description": "Updated description...",
  "address": "123 Main St, Mumbai, Maharashtra 400001",
  "contact_phone": "+919876543210",
  "website": "https://spicebazaar-finedining.com"
}
```

### Response
```json
{
  "message": "Business updated successfully"
}
```

## Get business categories
`GET /api/businesses/categories`

### Query Parameters
- `include_count` (boolean, optional) - Include business count in each category

### Response
```json
[
  {
    "id": 1,
    "name": "Restaurant",
    "description": "Dining and food services",
    "icon": "restaurant.png",
    "business_count": 45
  },
  {
    "id": 2,
    "name": "Retail",
    "description": "Shops and retail stores",
    "icon": "retail.png",
    "business_count": 32
  },
  {
    "id": 3,
    "name": "Professional Services",
    "description": "Legal, accounting, and professional services",
    "icon": "services.png",
    "business_count": 28
  }
]
```
- `description`