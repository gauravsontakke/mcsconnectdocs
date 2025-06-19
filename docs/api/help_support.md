# Help & Support API

## Get FAQs
`GET /api/help/faqs`

### Query Parameters
- `category` (string, optional) - Filter by category (e.g., 'account', 'billing', 'general')
- `search` (string, optional) - Search term to filter FAQs

### Response
```json
{
  "categories": [
    {
      "id": "account",
      "name": "Account",
      "icon": "account.png",
      "faqs": [
        {
          "id": "faq-101",
          "question": "How do I reset my password?",
          "answer": "You can reset your password by clicking on 'Forgot Password' on the login page and following the instructions sent to your email.",
          "last_updated": "2024-01-15T10:30:00Z"
        },
        {
          "id": "faq-102",
          "question": "How do I update my email address?",
          "answer": "Go to your account settings, click on 'Edit Profile', update your email address, and save the changes. You'll need to verify your new email address.",
          "last_updated": "2024-02-20T14:15:00Z"
        }
      ]
    },
    {
      "id": "billing",
      "name": "Billing",
      "icon": "billing.png",
      "faqs": [
        {
          "id": "faq-201",
          "question": "What payment methods do you accept?",
          "answer": "We accept all major credit/debit cards, UPI, and net banking. International payments are also accepted.",
          "last_updated": "2024-03-10T09:45:00Z"
        }
      ]
    }
  ],
  "popular": [
    "faq-101",
    "faq-201"
  ]
}
```

## Submit contact form
`POST /api/help/contact`

### Request Body
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "phone": "+919876543210",
  "subject": "Account access issue",
  "message": "I'm unable to access my account despite resetting my password.",
  "department": "technical_support",
  "priority": "high",
  "attachments": [
    {
      "name": "screenshot.png",
      "type": "image/png",
      "url": "https://example.com/uploads/screenshot123.png"
    }
  ]
}
```

### Response
```json
{
  "ticket_id": "TKT-789012",
  "message": "Your support request has been received. Our team will get back to you within 24 hours.",
  "support_email": "support@mcsconnect.com",
  "estimated_response_time": "24 hours"
}
```

## Get emergency contacts
`GET /api/emergency/contacts`

### Query Parameters
- `location` (string, optional) - Filter by location/city
- `category` (string, optional) - Filter by category (e.g., 'medical', 'police', 'fire', 'embassy')

### Response
```json
{
  "location": "Mumbai, Maharashtra",
  "last_updated": "2024-05-01T00:00:00Z",
  "contacts": [
    {
      "id": "ec-101",
      "name": "Police Control Room",
      "category": "police",
      "numbers": ["100", "112"],
      "description": "Emergency police assistance",
      "operating_hours": "24/7"
    },
    {
      "id": "ec-102",
      "name": "Ambulance / Medical Emergency",
      "category": "medical",
      "numbers": ["102", "108"],
      "description": "Medical emergency and ambulance services",
      "operating_hours": "24/7"
    },
    {
      "id": "ec-103",
      "name": "Fire Brigade",
      "category": "fire",
      "numbers": ["101"],
      "description": "Fire and rescue services",
      "operating_hours": "24/7"
    },
    {
      "id": "ec-104",
      "name": "Tourist Helpline",
      "category": "tourism",
      "numbers": ["1363"],
      "description": "24/7 tourist helpline in multiple languages",
      "operating_hours": "24/7"
    },
    {
      "id": "ec-105",
      "name": "US Consulate General Mumbai",
      "category": "embassy",
      "numbers": ["+91-22-2672-4000"],
      "email": "acs.mumbai@state.gov",
      "address": "C-49, G-Block, Bandra Kurla Complex, Bandra East, Mumbai 400051",
      "website": "https://in.usembassy.gov/embassy-consulates/mumbai/",
      "operating_hours": "Mon-Fri: 8:30 AM - 5:00 PM"
    }
  ]
}
```

## Create support ticket
`POST /api/help/support-ticket`

### Headers
```
Authorization: Bearer <token>
Content-Type: application/json
```

### Request Body
```json
{
  "subject": "Payment not processed",
  "description": "I made a payment 3 days ago but it's still showing as pending in my account.",
  "category": "billing",
  "priority": "high",
  "order_reference": "ORD-789012",
  "attachments": [
    {
      "name": "payment_receipt.pdf",
      "type": "application/pdf",
      "url": "https://example.com/uploads/receipt123.pdf"
    }
  ]
}
```

### Response
```json
{
  "ticket_id": "TKT-345678",
  "status": "open",
  "priority": "high",
  "assigned_to": "Support Team",
  "created_at": "2024-06-19T11:30:45Z",
  "message": "Your support ticket has been created. Our team will review your request and get back to you soon.",
  "estimated_response_time": "4 hours"
}
```
