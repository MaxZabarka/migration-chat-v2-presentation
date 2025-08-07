---

# Add message and create conversation endpoint

<div class="text-2xs slide-34-small-code" style="font-size: 0.65rem;">

<div class="grid grid-cols-2 gap-6">

<div>

### POST `/api/messages`

**The migration-friendly endpoint** - combines conversation lookup/creation AND message sending in one call. Designed to be similar to old /v2/complete endpoint

**What it does:**
1. Finds existing conversation (like `GET /api/conversations`)
2. OR creates new conversation (like `POST /api/conversations`)  
3. Adds your message to the conversation
4. Returns conversation details immediately
5. ALSO sends bot response via webhook

**Webhook Payload:**
```json
{
  "conversation_id": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
  "message": {
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "text": "Hey there! Can't wait to hear from you 😘",
    "from_bot": true,
    "sent_at": 1705327920,
    "attached_media": {
      "url": "https://example.com/flirty-selfie.jpg",
      "content_id": "b2c3d4e5-f6a7-8901-bcde-f23456789012"
    }
  }
}
```

</div>

<div>

```json
{
  "message": {
    "text": "Hey babe, miss me? 😘",
    "from_bot": false
  },
  // auto create a conversation if it doesn't already exist
  "conversation_creation_params": {
    "bot_id": "550e8400-e29b-41d4-a716-446655440000",
    "user_id": "user_123",
    "create_user_if_not_exists": true,
    "webhook": "https://example.com/webhook",
    "with_messages": [
      {
        "text": "Hey gorgeous! I've been thinking about you 💕",
        "from_bot": true
      }
    ]
  }
}
```

**Response:**
```json
{
  "conversation": {
    "id": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
    "bot_id": "550e8400-e29b-41d4-a716-446655440000",
    "user_id": "user_123",
    "messages": [...]
  },
  "created_conversation": false
}
```

</div>

</div>

</div>
