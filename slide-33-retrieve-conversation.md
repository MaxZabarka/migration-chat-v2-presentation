---

# Retrieving Conversations

<div class="grid grid-cols-2 gap-6 text-sm">

<div>

## GET `/api/conversations/{id}`

Fetches a specific conversation with full message history.


</div>

<div>

```http
GET /api/conversations/f47ac10b-58cc-4372-a567-0e02b2c3d479
```

**Response:**
```json
{
  "bot_id": "550e8400-e29b-41d4-a716-446655440000",
  "user_id": "user_123",
  "messages": [
    {
      "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
      "text": "Hey gorgeous! Missing you already 💕",
      "from_bot": true,
      "sent_at": 1705327800,
      "attached_media": null
    },
    {
      "id": "b2c3d4e5-f6a7-8901-bcde-f23456789012", 
      "text": "I've been thinking about you too 😘",
      "from_bot": false,
      "sent_at": 1705327860,
      "attached_media": null
    }
  ]
}
```

</div>

</div>
