---

# Summary: Endpoint Comparison V1 vs V3

<div class="grid grid-cols-2 gap-6 text-sm">

<div>

## V1: Single Complete Endpoint

**POST** `dev-api.prioros.com/v2/complete`

```json
{
  "conversation_id": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
  "bot_id": "550e8400-e29b-41d4-a716-446655440000",
  "message": "Hey babe, what's up? 😘",
  "messages": [
    {
      "bot": true, 
      "content": ["Hi gorgeous!", "Missing you already 💕"]
    },
    {
      "bot": false,
      "content": ["I miss you too!"]
    }
  ],
  "webhook": "https://api.example.com/webhook"
}
```

</div>

<div>

## V3: New Message Endpoint

**POST** `dev-api.prioros.com/v3/api/messages`

```json
{
  "message": {
    "text": "Hey babe, what's up? 😘",
    "from_bot": false
  },
  "user_id": "user_123",
  "bot_id": "550e8400-e29b-41d4-a716-446655440000",
  "create_user_if_not_exists": true,
  "conversation_creation_params": {
    "bot_id": "550e8400-e29b-41d4-a716-446655440000",
    "user_id": "user_123",
    "webhook": "https://api.example.com/webhook",
    "with_messages": [
      {"text": "Hi gorgeous!", "from_bot": true},
      {"text": "Missing you already 💕", "from_bot": true},
      {"text": "I miss you too!", "from_bot": false}
    ]
  }
}
```

</div>

</div>

<div class="mt-4 p-3 bg-blue-50 border-l-4 border-blue-500 text-blue-900 text-xs">
<strong>Key Changes:</strong> conversation_id → user_id for identification, segmented messages → atomic messages, nested conversation_creation_params
</div>