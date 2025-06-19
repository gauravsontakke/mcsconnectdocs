# Marketplace API

## Get all marketplace items
`GET /api/marketplace/items`

### Query Parameters
- `page` (number, optional, default: 1) - Page number
- `page_size` (number, optional, default: 10) - Items per page
- `category` (string, optional) - Filter by category ID
- `sort_by` (string, optional) - Field to sort by (e.g., 'price', 'date_posted')
- `sort_order` (string, optional) - Sort order ('asc' or 'desc')
- `search` (string, optional) - Search term

### Response
```json
{
  "items": [
    {
      "id": 1,
      "title": "Used iPhone 12",
      "description": "In excellent condition, 1 year old",
      "price": 45000,
      "currency": "INR",
      "category_id": 5,
      "seller_id": 123,
      "condition": "used",
      "images": ["image1.jpg", "image2.jpg"],
      "location": "Mumbai",
      "created_at": "2025-05-15T10:30:00Z",
      "status": "available"
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

## Get item details
`GET /api/marketplace/items/{id}`

### Path Parameters
- `id` (required) - ID of the marketplace item

### Response
```json
{
  "id": 1,
  "title": "Used iPhone 12",
  "description": "In excellent condition, 1 year old. No scratches, battery health 92%.",
  "price": 45000,
  "currency": "INR",
  "category": {
    "id": 5,
    "name": "Electronics",
    "icon": "electronics.png"
  },
  "seller": {
    "id": 123,
    "name": "John Doe",
    "rating": 4.8,
    "member_since": "2023-01-15"
  },
  "condition": "used",
  "images": ["image1.jpg", "image2.jpg"],
  "location": "Mumbai",
  "created_at": "2025-05-15T10:30:00Z",
  "updated_at": "2025-05-16T09:15:00Z",
  "status": "available",
  "view_count": 45
}
```

## Create new listing
`POST /api/marketplace/items`

### Headers
```
Authorization: Bearer <token>
Content-Type: multipart/form-data
```

### Request Body (form-data)
- `title` (string, required) - Item title
- `description` (string, required) - Detailed description
- `price` (number, required) - Price in INR
- `category_id` (number, required) - Category ID
- `condition` (string, required) - 'new', 'used', or 'refurbished'
- `location` (string, required) - Item location
- `images` (file[], optional) - Upload images (max 5)
- `contact_phone` (string, optional) - Contact phone number

### Response
```json
{
  "id": 1,
  "message": "Listing created successfully",
  "images_uploaded": 2
}
```

## Update listing
`PUT /api/marketplace/items/{id}`

### Headers
```
Authorization: Bearer <token>
Content-Type: application/json
```

### Path Parameters
- `id` (required) - ID of the listing to update

### Request Body
```json
{
  "title": "Used iPhone 12 - Like New",
  "description": "Updated description...",
  "price": 43000,
  "status": "sold"
}
```

### Response
```json
{
  "message": "Listing updated successfully"
}
```

## Delete listing
`DELETE /api/marketplace/items/{id}`

### Headers
```
Authorization: Bearer <token>
```

### Path Parameters
- `id` (required) - ID of the listing to delete

### Response
```json
{
  "message": "Listing deleted successfully"
}
```

## Get marketplace categories
`GET /api/marketplace/categories`

### Response
```json
[
  {
    "id": 1,
    "name": "Electronics",
    "description": "Mobile phones, laptops, gadgets",
    "icon": "electronics.png",
    "item_count": 124
  },
  {
    "id": 2,
    "name": "Furniture",
    "description": "Home and office furniture",
    "icon": "furniture.png",
    "item_count": 78
  }
]
```
