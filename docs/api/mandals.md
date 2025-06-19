# Mandals API

## Get Maharashtra Mandal chapters
`GET /api/mandals`

### Query Parameters
- `page` (number, optional, default: 1) - Page number
- `page_size` (number, optional, default: 10) - Items per page
- `region` (string, optional) - Filter by region (e.g., 'North America', 'Europe')
- `search` (string, optional) - Search term for mandal name or location
- `sort_by` (string, optional) - Field to sort by (e.g., 'name', 'established_year')
- `sort_order` (string, optional) - Sort order ('asc' or 'desc')

### Response
```json
{
  "mandals": [
    {
      "id": 1,
      "name": "Mumbai Marathi Mandal",
      "location": "Mumbai, India",
      "region": "India",
      "established_year": 1985,
      "logo": "mmm-logo.png",
      "description": "One of the oldest Marathi Mandals in Mumbai, organizing cultural events and community services.",
      "member_count": 1250,
      "website": "https://mumbaimarathimandal.org",
      "social_media": {
        "facebook": "mumbaimarathimandal",
        "instagram": "mmmumbai"
      },
      "is_active": true,
      "next_event": {
        "id": 101,
        "title": "Ganesh Utsav 2024",
        "date": "2024-09-07",
        "location": "Shivaji Park, Mumbai"
      }
    },
    {
      "id": 2,
      "name": "Maharashtra Mandal New York",
      "location": "New York, USA",
      "region": "North America",
      "established_year": 1995,
      "logo": "mmny-logo.png",
      "description": "Connecting Maharashtrians in the New York tri-state area through cultural and social events.",
      "member_count": 850,
      "website": "https://maharashtramandalny.org",
      "social_media": {
        "facebook": "maharashtramandalny",
        "instagram": "maharashtramandalny"
      },
      "is_active": true,
      "next_event": {
        "id": 205,
        "title": "Gudi Padwa Celebration",
        "date": "2024-04-09",
        "location": "Queens, NY"
      }
    }
  ],
  "pagination": {
    "total_items": 2,
    "total_pages": 1,
    "current_page": 1,
    "page_size": 10
  }
}
```

## Get mandal details
`GET /api/mandals/{id}`

### Path Parameters
- `id` (required) - ID of the mandal

### Response
```json
{
  "id": 1,
  "name": "Mumbai Marathi Mandal",
  "location": "Mumbai, India",
  "address": {
    "street": "123 Shivaji Marg",
    "city": "Mumbai",
    "state": "Maharashtra",
    "country": "India",
    "postal_code": "400028",
    "coordinates": {
      "lat": 19.0760,
      "lng": 72.8777
    }
  },
  "region": "India",
  "established_year": 1985,
  "registration_number": "MH/1234/1985",
  "logo": "mmm-logo.png",
  "banner_image": "mmm-banner.jpg",
  "description": "One of the oldest Marathi Mandals in Mumbai, organizing cultural events and community services.",
  "mission": "To preserve and promote Marathi culture and provide a platform for community members to connect and celebrate their heritage.",
  "activities": [
    "Cultural events",
    "Religious celebrations",
    "Educational programs",
    "Social services",
    "Youth activities"
  ],
  "member_count": 1250,
  "contact": {
    "email": "info@mumbaimarathimandal.org",
    "phone": "+912234567890",
    "website": "https://mumbaimarathimandal.org",
    "social_media": {
      "facebook": "mumbaimarathimandal",
      "instagram": "mmmumbai",
      "twitter": "mmmumbai",
      "youtube": "mumbaimarathimandal"
    }
  },
  "meeting_schedule": "First Sunday of every month at 6:00 PM",
  "meeting_location": "Shivaji Mandir, Dadar",
  "is_active": true,
  "founding_members": [
    {
      "name": "Vijay Joshi",
      "role": "Founder & First President"
    },
    {
      "name": "Meera Deshpande",
      "role": "Co-Founder"
    }
  ],
  "current_leadership": [
    {
      "name": "Rajesh Patil",
      "position": "President",
      "term": "2023-2025"
    },
    {
      "name": "Priya Kulkarni",
      "position": "Secretary",
      "term": "2023-2025"
    },
    {
      "name": "Amit Deshmukh",
      "position": "Treasurer",
      "term": "2023-2025"
    }
  ],
  "upcoming_events": [
    {
      "id": 101,
      "title": "Ganesh Utsav 2024",
      "date": "2024-09-07",
      "time": "09:00 AM - 09:00 PM",
      "location": "Shivaji Park, Mumbai",
      "description": "Annual Ganesh Utsav celebration with cultural programs and prasad distribution.",
      "registration_required": true
    },
    {
      "id": 102,
      "title": "Marathi Bhasha Diwas",
      "date": "2024-02-27",
      "time": "06:00 PM - 09:00 PM",
      "location": "Mandal Office, Dadar",
      "description": "Celebration of Marathi Language Day with poetry, speeches, and cultural performances.",
      "registration_required": false
    }
  ],
  "gallery": [
    {
      "id": "img1",
      "url": "gallery/event1.jpg",
      "caption": "Ganesh Utsav 2023",
      "date": "2023-09-10"
    },
    {
      "id": "img2",
      "url": "gallery/event2.jpg",
      "caption": "Diwali Celebration",
      "date": "2023-11-12"
    }
  ],
  "created_at": "1985-05-15T00:00:00Z",
  "updated_at": "2024-01-10T15:30:00Z"
}
```

## Get mandal members
`GET /api/mandals/{id}/members`

### Headers
```
Authorization: Bearer <token>
```

### Path Parameters
- `id` (required) - ID of the mandal

### Query Parameters
- `page` (number, optional, default: 1) - Page number
- `page_size` (number, optional, default: 20) - Items per page
- `search` (string, optional) - Search term for member name or email
- `role` (string, optional) - Filter by role (e.g., 'member', 'board_member', 'volunteer')
- `joined_after` (string, optional) - Filter members who joined after this date (YYYY-MM-DD)
- `sort_by` (string, optional) - Field to sort by (e.g., 'name', 'join_date')
- `sort_order` (string, optional) - Sort order ('asc' or 'desc')

### Response
```json
{
  "mandal_id": 1,
  "mandal_name": "Mumbai Marathi Mandal",
  "members": [
    {
      "id": 1001,
      "member_id": "MMM-2023-1001",
      "first_name": "Rajesh",
      "last_name": "Patil",
      "email": "rajesh.patil@example.com",
      "phone": "+919876543210",
      "profile_picture": "profiles/rajesh.jpg",
      "role": "president",
      "is_board_member": true,
      "designation": "President",
      "join_date": "2015-03-10",
      "membership_status": "active",
      "address": {
        "street": "456 Shivaji Nagar",
        "city": "Mumbai",
        "state": "Maharashtra",
        "country": "India",
        "postal_code": "400028"
      },
      "profession": "Business Owner",
      "company": "Patil Enterprises",
      "birth_date": "1980-07-15",
      "anniversary_date": "2005-05-20",
      "interests": ["theater", "music", "social_work"],
      "skills": ["public_speaking", "event_management"],
      "volunteer_roles": ["event_coordinator", "mc"],
      "last_active": "2024-01-15T14:30:00Z",
      "social_media": {
        "facebook": "rajesh.patil.123",
        "linkedin": "in/rajeshpatil"
      },
      "bio": "Passionate about preserving Marathi culture and serving the community.",
      "is_profile_public": true,
      "created_at": "2015-03-10T10:15:30Z",
      "updated_at": "2024-01-10T09:45:00Z"
    },
    {
      "id": 1002,
      "member_id": "MMM-2022-0876",
      "first_name": "Priya",
      "last_name": "Kulkarni",
      "email": "priya.k@example.com",
      "profile_picture": "profiles/priya.jpg",
      "role": "secretary",
      "is_board_member": true,
      "designation": "Secretary",
      "join_date": "2018-06-22",
      "membership_status": "active",
      "is_profile_public": false,
      "created_at": "2018-06-22T14:20:00Z",
      "updated_at": "2023-12-15T11:30:00Z"
    }
  ],
  "pagination": {
    "total_members": 1250,
    "active_members": 980,
    "board_members": 12,
    "total_pages": 63,
    "current_page": 1,
    "page_size": 20
  },
  "member_roles": [
    {"id": "president", "name": "President", "count": 1},
    {"id": "vice_president", "name": "Vice President", "count": 1},
    {"id": "secretary", "name": "Secretary", "count": 1},
    {"id": "treasurer", "name": "Treasurer", "count": 1},
    {"id": "board_member", "name": "Board Member", "count": 8},
    {"id": "member", "name": "General Member", "count": 968}
  ],
  "member_statistics": {
    "by_gender": {
      "male": 620,
      "female": 600,
      "other": 30
    },
    "by_age_group": {
      "under_18": 50,
      "18_25": 180,
      "26_35": 400,
      "36_50": 450,
      "51_65": 150,
      "over_65": 20
    },
    "by_join_year": {
      "2024": 45,
      "2023": 120,
      "2022": 150,
      "2021": 180,
      "2020": 200,
      "before_2020": 555
    }
  }
}
```

## Get mandal events
`GET /api/mandals/{id}/events`

### Path Parameters
- `id` (required) - ID of the mandal

### Query Parameters
- `type` (string, optional) - Filter by event type (e.g., 'cultural', 'religious', 'social')
- `status` (string, optional) - Filter by status ('upcoming', 'past', 'ongoing')
- `start_date` (string, optional) - Filter events on or after this date (YYYY-MM-DD)
- `end_date` (string, optional) - Filter events on or before this date (YYYY-MM-DD)
- `featured` (boolean, optional) - Filter featured events only
- `page` (number, optional, default: 1) - Page number
- `page_size` (number, optional, default: 10) - Items per page

### Response
```json
{
  "mandal_id": 1,
  "mandal_name": "Mumbai Marathi Mandal",
  "events": [
    {
      "id": 101,
      "title": "Ganesh Utsav 2024",
      "description": "Annual Ganesh Utsav celebration with cultural programs and prasad distribution.",
      "type": "religious",
      "category": "festival",
      "start_datetime": "2024-09-07T09:00:00+05:30",
      "end_datetime": "2024-09-07T21:00:00+05:30",
      "timezone": "Asia/Kolkata",
      "location": {
        "name": "Shivaji Park",
        "address": "Shivaji Park, Dadar West, Mumbai, Maharashtra 400028",
        "coordinates": {
          "lat": 19.0417,
          "lng": 72.8419
        },
        "landmark": "Near Shivaji Statue"
      },
      "organizer": {
        "id": 1,
        "name": "Mumbai Marathi Mandal",
        "contact_person": "Rajesh Patil",
        "contact_phone": "+919876543210",
        "contact_email": "events@mumbaimarathimandal.org"
      },
      "image": "events/ganesh-utsav-2024.jpg",
      "banner_image": "events/banner-ganesh-utsav-2024.jpg",
      "registration_required": true,
      "registration_deadline": "2024-09-05T23:59:59+05:30",
      "registration_url": "https://mumbaimarathimandal.org/events/ganesh-utsav-2024/register",
      "max_participants": 500,
      "registered_participants": 342,
      "waitlist_count": 28,
      "price": {
        "member": 0,
        "non_member": 200,
        "child": 0,
        "senior_citizen": 100,
        "currency": "INR"
      },
      "tags": ["religious", "festival", "family"],
      "status": "upcoming",
      "is_featured": true,
      "schedule": [
        {
          "time": "09:00 - 10:30",
          "activity": "Ganpati Sthapana & Pooja",
          "speaker": "Shri. Deshpande Guruji"
        },
        {
          "time": "11:00 - 13:00",
          "activity": "Cultural Program - Bhajans"
        },
        {
          "time": "13:00 - 14:00",
          "activity": "Mahaprasad Lunch"
        },
        {
          "time": "15:00 - 18:00",
          "activity": "Cultural Program - Dance & Drama"
        },
        {
          "time": "19:00 - 21:00",
          "activity": "Aarti & Visarjan"
        }
      ],
      "sponsors": [
        {
          "name": "Patil Constructions",
          "logo": "sponsors/patil-constructions.png",
          "level": "platinum"
        },
        {
          "name": "Maharashtra Bank",
          "logo": "sponsors/maharashtra-bank.png",
          "level": "gold"
        }
      ],
      "social_media_hashtags": ["#MMMGaneshUtsav2024", "#MumbaiMarathiMandal"],
      "created_at": "2023-12-01T10:00:00Z",
      "updated_at": "2024-01-05T15:30:00Z",
      "created_by": 1001,
      "updated_by": 1002
    }
  ],
  "pagination": {
    "total_events": 1,
    "upcoming_events": 1,
    "past_events": 0,
    "total_pages": 1,
    "current_page": 1,
    "page_size": 10
  },
  "event_statistics": {
    "by_type": [
      {"type": "cultural", "count": 12},
      {"type": "religious", "count": 8},
      {"type": "social", "count": 5},
      {"type": "educational", "count": 3}
    ],
    "by_month": [
      {"month": "2024-01", "count": 2},
      {"month": "2024-02", "count": 1},
      {"month": "2024-03", "count": 3},
      {"month": "2024-09", "count": 1}
    ],
    "total_participants": 1250,
    "average_attendance_rate": 78.5
  }
}
```
