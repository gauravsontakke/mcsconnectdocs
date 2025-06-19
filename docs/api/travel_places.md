# Travel & Places API

## Get travel partners
`GET /api/travel/partners`

### Query Parameters
- `type` (string, optional) - Filter by partner type (e.g., 'hotel', 'travel_agency', 'car_rental')
- `location` (string, optional) - Filter by location
- `page` (number, optional, default: 1) - Page number
- `page_size` (number, optional, default: 10) - Items per page

### Response
```json
{
  "partners": [
    {
      "id": 1,
      "name": "Maharashtra Travels",
      "type": "travel_agency",
      "description": "Specialized in Maharashtra tourism packages",
      "contact_phone": "+919876543210",
      "website": "https://maharashtratravels.com",
      "address": "456 Travel St, Mumbai",
      "rating": 4.7,
      "is_verified": true,
      "logo": "partner1.jpg"
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

## Get places of interest
`GET /api/places`

### Query Parameters
- `category` (string, optional) - Filter by category ID
- `location` (string, optional) - Filter by location (city/region)
- `search` (string, optional) - Search term for place name or description
- `page` (number, optional, default: 1) - Page number
- `page_size` (number, optional, default: 10) - Items per page
- `sort_by` (string, optional) - Field to sort by (e.g., 'name', 'rating')
- `sort_order` (string, optional) - Sort order ('asc' or 'desc')

### Response
```json
{
  "places": [
    {
      "id": 1,
      "name": "Gateway of India",
      "description": "Historic monument in Mumbai",
      "category_id": 2,
      "address": "Apollo Bandar, Colaba, Mumbai",
      "location": {
        "lat": 18.9220,
        "lng": 72.8347
      },
      "contact_phone": "+912222627000",
      "opening_hours": "Open 24 hours",
      "entry_fee": 0,
      "avg_visit_duration": "1-2 hours",
      "images": ["gateway1.jpg", "gateway2.jpg"],
      "rating": 4.8,
      "review_count": 1250,
      "is_featured": true,
      "tags": ["historical", "landmark", "photography"]
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

## Get place categories
`GET /api/places/categories`

### Response
```json
[
  {
    "id": 1,
    "name": "Historical Sites",
    "description": "Ancient monuments and historical landmarks",
    "icon": "history.png"
  },
  {
    "id": 2,
    "name": "Parks & Nature",
    "description": "National parks and natural attractions",
    "icon": "nature.png"
  },
  {
    "id": 3,
    "name": "Museums",
    "description": "Art, history, and science museums",
    "icon": "museum.png"
  },
  {
    "id": 4,
    "name": "Religious Sites",
    "description": "Temples, churches, mosques, and other places of worship",
    "icon": "temple.png"
  },
  {
    "id": 5,
    "name": "Shopping",
    "description": "Markets and shopping districts",
    "icon": "shopping.png"
  }
]
```

## Request travel assistance
`POST /api/travel/assistance`

### Headers
```
Authorization: Bearer <token>
Content-Type: application/json
```

### Request Body
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "phone": "+919876543210",
  "trip_type": "family_vacation",
  "destination": "Mumbai, Maharashtra",
  "travel_dates": {
    "start": "2025-08-15",
    "end": "2025-08-25"
  },
  "adults": 2,
  "children": 1,
  "budget_range": {
    "currency": "INR",
    "min": 50000,
    "max": 75000
  },
  "special_requirements": "Need wheelchair accessible accommodation",
  "interests": ["beaches", "historical_sites", "local_cuisine"],
  "additional_notes": "Interested in cultural experiences and local festivals during our stay"
}
```

### Response
```json
{
  "request_id": "TRAVEL-789012",
  "message": "Travel assistance request received. Our team will contact you within 24 hours.",
  "next_steps": [
    "Check your email for a confirmation",
    "Our travel consultant will contact you to discuss your requirements",
    "Receive a customized travel itinerary"
  ]
}
```
