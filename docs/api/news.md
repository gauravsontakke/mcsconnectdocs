# News API

## Get all news articles
`GET /api/news`

### Query Parameters
- `page` (number, optional, default: 1) - Page number for pagination
- `page_size` (number, optional, default: 10) - Number of items per page
- `sort_by` (string, optional) - Field to sort by (e.g., 'date', 'title')
- `sort_order` (string, optional) - Sort order ('asc' or 'desc')
- `category` (string, optional) - Filter by category

### Response
```json
[
  {
    "id": 101,
    "title": "Big News!",
    "description": "Breaking news content...",
    "category": "Politics",
    "icon": "news-icon.png",
    "news_page_url": "/news/101"
  }
]
```

## Get news article details
`GET /api/news/{id}`

### Path Parameters
- `id` (required) - ID of the news article

### Response
```json
{
  "id": 101,
  "title": "Big News!",
  "description": "Full news content...",
  "category": "Politics",
  "icon": "news-icon.png",
  "news_page_url": "/news/101"
}
```

## Get news categories
`GET /api/news/categories`

### Query Parameters
- `page` (number, optional, default: 1)
- `page_size` (number, optional, default: 10)
- `sort_by` (string, optional)
- `sort_order` (string, optional)

### Response
```json
[
  {
    "id": 1,
    "name": "Politics",
    "description": "Political news and updates",
    "icon": "politics-icon.png"
  }
]
```

## Filter news by category
`GET /api/news?category={category}`

### Query Parameters
- `category` (required) - Category to filter by
- `page` (number, optional, default: 1)
- `page_size` (number, optional, default: 10)
- `sort_by` (string, optional)
- `sort_order` (string, optional)

### Response
```json
[
  {
    "id": 102,
    "title": "Economy on the Rise",
    "description": "Economic updates...",
    "category": "Finance",
    "icon": "finance-icon.png",
    "news_page_url": "/news/102"
  }
]
```
- `published_date`