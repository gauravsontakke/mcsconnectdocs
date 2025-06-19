# Search API

## Global search
`GET /api/search`

### Query Parameters
- `q` (string, required) - Search query
- `types` (string, optional) - Comma-separated list of content types to search (e.g., 'events,businesses,news')
- `location` (string, optional) - Filter by location
- `category` (string, optional) - Filter by category ID
- `page` (number, optional, default: 1) - Page number
- `page_size` (number, optional, default: 10) - Items per page
- `sort_by` (string, optional) - Field to sort by (e.g., 'relevance', 'date', 'name')
- `sort_order` (string, optional) - Sort order ('asc' or 'desc')
- `filters` (JSON string, optional) - Advanced filters as JSON object

### Response
```json
{
  "query": "marathi",
  "total_results": 45,
  "took_ms": 120,
  "results": [
    {
      "type": "event",
      "id": 301,
      "title": "Marathi Cultural Festival 2024",
      "description": "Annual celebration of Marathi culture with music, dance, and food.",
      "date": "2024-07-15T18:00:00+05:30",
      "location": "Mumbai, India",
      "image": "events/marathi-festival-2024.jpg",
      "score": 0.98,
      "highlight": {
        "title": ["<em>Marathi</em> Cultural Festival 2024"],
        "description": ["Annual celebration of <em>Marathi</em> culture with music, dance, and food."]
      }
    },
    {
      "type": "business",
      "id": 42,
      "name": "Marathi Bhojanalaya",
      "description": "Authentic Maharashtrian restaurant serving traditional dishes.",
      "category": "Restaurant",
      "location": "Pune, India",
      "rating": 4.7,
      "image": "businesses/marathi-bhojanalaya.jpg",
      "score": 0.95,
      "highlight": {
        "name": ["<em>Marathi</em> Bhojanalaya"],
        "description": ["Authentic Maharashtrian restaurant serving traditional dishes."]
      }
    },
    {
      "type": "news",
      "id": 78,
      "title": "Marathi Film Wins National Award",
      "description": "Local Marathi language film 'Sairat' wins big at the 64th National Film Awards.",
      "date": "2024-04-07T10:30:00+05:30",
      "category": "Entertainment",
      "image": "news/marathi-film-award.jpg",
      "score": 0.92,
      "highlight": {
        "title": ["<em>Marathi</em> Film Wins National Award"],
        "description": ["Local <em>Marathi</em> language film 'Sairat' wins big at the 64th National Film Awards."]
      }
    }
  ],
  "facets": {
    "types": [
      {"type": "event", "count": 12, "selected": false},
      {"type": "business", "count": 18, "selected": false},
      {"type": "news", "count": 10, "selected": false},
      {"type": "mandal", "count": 5, "selected": false}
    ],
    "categories": [
      {"id": 1, "name": "Food & Dining", "count": 15, "selected": false},
      {"id": 2, "name": "Entertainment", "count": 12, "selected": false},
      {"id": 3, "name": "Community", "count": 10, "selected": false},
      {"id": 4, "name": "Shopping", "count": 8, "selected": false}
    ],
    "locations": [
      {"name": "Mumbai", "count": 20, "selected": false},
      {"name": "Pune", "count": 12, "selected": false},
      {"name": "Nashik", "count": 8, "selected": false},
      {"name": "Nagpur", "count": 5, "selected": false}
    ]
  },
  "pagination": {
    "total_items": 45,
    "total_pages": 5,
    "current_page": 1,
    "page_size": 10,
    "has_next": true,
    "has_previous": false
  }
}
```

## Get search suggestions
`GET /api/search/suggestions`

### Query Parameters
- `q` (string, required) - Search query (minimum 2 characters)
- `limit` (number, optional, default: 5) - Maximum number of suggestions to return
- `types` (string, optional) - Comma-separated list of content types to suggest from (e.g., 'events,businesses,news')
- `popular` (boolean, optional) - Include popular searches (default: false)

### Response
```json
{
  "query": "mar",
  "suggestions": [
    {
      "type": "suggestion",
      "text": "marathi",
      "score": 0.95,
      "highlight": "<em>Mar</em>athi",
      "count": 45
    },
    {
      "type": "suggestion",
      "text": "marriage hall",
      "score": 0.85,
      "highlight": "<em>Mar</em>riage hall",
      "count": 12
    },
    {
      "type": "suggestion",
      "text": "marine lines",
      "score": 0.78,
      "highlight": "<em>Mar</em>ine lines",
      "count": 8
    },
    {
      "type": "popular",
      "text": "marathon 2024",
      "score": 0.0,
      "highlight": "<em>Mar</em>athon 2024",
      "count": 0
    },
    {
      "type": "recent",
      "text": "marathi classes",
      "score": 0.0,
      "highlight": "<em>Mar</em>athi classes",
      "count": 0
    }
  ],
  "categories": [
    {
      "type": "category",
      "id": 5,
      "name": "Marathi",
      "count": 15,
      "highlight": "<em>Mar</em>athi"
    },
    {
      "type": "category",
      "id": 12,
      "name": "Marriage Halls",
      "count": 8,
      "highlight": "<em>Mar</em>riage Halls"
    }
  ],
  "entities": [
    {
      "type": "business",
      "id": 42,
      "name": "Marathi Bhojanalaya",
      "category": "Restaurant",
      "location": "Pune",
      "image": "businesses/marathi-bhojanalaya-thumb.jpg",
      "highlight": "<em>Mar</em>athi Bhojanalaya"
    },
    {
      "type": "event",
      "id": 301,
      "name": "Marathi Cultural Festival 2024",
      "date": "2024-07-15",
      "location": "Mumbai",
      "image": "events/marathi-festival-thumb.jpg",
      "highlight": "<em>Mar</em>athi Cultural Festival 2024"
    }
  ]
}
```

## Advanced search
`POST /api/search/advanced`

### Headers
```
Content-Type: application/json
```

### Request Body
```json
{
  "query": {
    "bool": {
      "must": [
        {
          "multi_match": {
            "query": "marathi culture",
            "fields": ["title^3", "description^2", "content"],
            "fuzziness": "AUTO"
          }
        }
      ],
      "filter": [
        {
          "terms": {
            "type": ["event", "news"]
          }
        },
        {
          "range": {
            "date": {
              "gte": "now-1y",
              "lte": "now+1M"
            }
          }
        },
        {
          "geo_distance": {
            "distance": "50km",
            "location": {
              "lat": 19.0760,
              "lon": 72.8777
            }
          }
        }
      ]
    }
  },
  "from": 0,
  "size": 10,
  "sort": [
    {
      "_score": {
        "order": "desc"
      }
    },
    {
      "date": {
        "order": "desc"
      }
    }
  ],
  "highlight": {
    "fields": {
      "title": {},
      "description": {},
      "content": {}
    }
  },
  "aggs": {
    "types": {
      "terms": {
        "field": "type"
      }
    },
    "categories": {
      "terms": {
        "field": "category"
      }
    },
    "locations": {
      "terms": {
        "field": "location.keyword",
        "size": 10
      }
    },
    "date_histogram": {
      "date_histogram": {
        "field": "date",
        "calendar_interval": "month"
      }
    }
  }
}
```

### Response
```json
{
  "took": 85,
  "timed_out": false,
  "_shards": {
    "total": 5,
    "successful": 5,
    "skipped": 0,
    "failed": 0
  },
  "hits": {
    "total": {
      "value": 27,
      "relation": "eq"
    },
    "max_score": 12.3456,
    "hits": [
      {
        "_index": "events",
        "_type": "_doc",
        "_id": "301",
        "_score": 12.3456,
        "_source": {
          "type": "event",
          "id": 301,
          "title": "Marathi Cultural Festival 2024",
          "description": "Annual celebration of Marathi culture with music, dance, and food.",
          "date": "2024-07-15T18:00:00+05:30",
          "location": "Mumbai, India",
          "category": "Cultural"
        },
        "highlight": {
          "title": ["<em>Marathi</em> Cultural Festival 2024"],
          "description": ["Annual celebration of <em>Marathi</em> <em>culture</em> with music, dance, and food."]
        }
      },
      {
        "_index": "news",
        "_type": "_doc",
        "_id": "78",
        "_score": 10.2345,
        "_source": {
          "type": "news",
          "id": 78,
          "title": "Marathi Culture Exhibition Draws Crowds",
          "description": "The week-long exhibition showcases the rich heritage of Marathi culture.",
          "date": "2024-05-20T10:00:00+05:30",
          "location": "Pune, India",
          "category": "Culture"
        },
        "highlight": {
          "title": ["<em>Marathi</em> <em>Culture</em> Exhibition Draws Crowds"],
          "description": ["The week-long exhibition showcases the rich heritage of <em>Marathi</em> <em>culture</em>."]
        }
      }
    ]
  },
  "aggregations": {
    "types": {
      "doc_count_error_upper_bound": 0,
      "sum_other_doc_count": 0,
      "buckets": [
        {
          "key": "event",
          "doc_count": 15
        },
        {
          "key": "news",
          "doc_count": 12
        }
      ]
    },
    "categories": {
      "doc_count_error_upper_bound": 0,
      "sum_other_doc_count": 0,
      "buckets": [
        {
          "key": "Cultural",
          "doc_count": 10
        },
        {
          "key": "Entertainment",
          "doc_count": 8
        },
        {
          "key": "Education",
          "doc_count": 5
        },
        {
          "key": "Food",
          "doc_count": 4
        }
      ]
    },
    "locations": {
      "doc_count_error_upper_bound": 0,
      "sum_other_doc_count": 0,
      "buckets": [
        {
          "key": "Mumbai, India",
          "doc_count": 15
        },
        {
          "key": "Pune, India",
          "doc_count": 8
        },
        {
          "key": "Nashik, India",
          "doc_count": 4
        }
      ]
    },
    "date_histogram": {
      "buckets": [
        {
          "key_as_string": "2024-01-01T00:00:00.000Z",
          "key": 1704067200000,
          "doc_count": 2
        },
        {
          "key_as_string": "2024-02-01T00:00:00.000Z",
          "key": 1706745600000,
          "doc_count": 3
        },
        {
          "key_as_string": "2024-03-01T00:00:00.000Z",
          "key": 1709251200000,
          "doc_count": 4
        },
        {
          "key_as_string": "2024-04-01T00:00:00.000Z",
          "key": 1711929600000,
          "doc_count": 3
        },
        {
          "key_as_string": "2024-05-01T00:00:00.000Z",
          "key": 1714521600000,
          "doc_count": 5
        },
        {
          "key_as_string": "2024-06-01T00:00:00.000Z",
          "key": 1717200000000,
          "doc_count": 3
        },
        {
          "key_as_string": "2024-07-01T00:00:00.000Z",
          "key": 1719792000000,
          "doc_count": 7
        }
      ]
    }
  }
}
```

## Get recent searches
`GET /api/search/recent`

### Headers
```
Authorization: Bearer <token>
```

### Query Parameters
- `limit` (number, optional, default: 10) - Maximum number of recent searches to return

### Response
```json
[
  {
    "query": "marathi classes",
    "timestamp": "2024-06-19T10:30:45Z",
    "result_count": 8
  },
  {
    "query": "marriage halls in pune",
    "timestamp": "2024-06-18T15:20:10Z",
    "result_count": 12
  },
  {
    "query": "marine drive restaurants",
    "timestamp": "2024-06-17T19:45:30Z",
    "result_count": 15
  }
]
```

## Clear search history
`DELETE /api/search/history`

### Headers
```
Authorization: Bearer <token>
```

### Response
```json
{
  "message": "Search history cleared successfully",
  "items_deleted": 42
}
```
