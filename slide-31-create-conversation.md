---

# Creating a Conversation

<div class="grid grid-cols-2 gap-6 text-sm">

<div>

## POST `/api/conversations`

Creates a new conversation between a user and bot. Automatically creates the user if they don't exist.

**Key Features:**
- Creates user if needed (`create_user_if_not_exists`)
- Optional initial messages with `with_messages`
- Webhook configuration for responses
- Returns conversation ID and initial state

</div>

<div>

```json
{
  "bot_id": "550e8400-e29b-41d4-a716-446655440000",
  "user_id": "user_123",
  "create_user_if_not_exists": true,
  "webhook": "https://example.com/webhook",
  "with_messages": [
    {
      "text": "Hey there! I've been thinking about you 😘",
      "from_bot": true
    }
  ]
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
  }
}
```

</div>

</div>