---

# Complete Message Generation: V1 vs V3

<div class="grid grid-cols-2 gap-4 text-xs">

<div>

## V1 - Single Request (Production Example)
```javascript
// Real production request to V1 API
const response = await fetch('/v2/complete', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer sk_prod_abcd1234...',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    "bot_id": "88d86507-8d6c-4fad-b6f6-15d4fd377c83",
    "message": "Hola",
    "user_id": "306066b7-e47a-405b-8726-ccec362858ac",
    "webhook": "https://api.qkkie.com/chat/clonetwin/messages?token=...",
    "language": "es",
    "platform": "Qkkie",
    "messages": [
      {
        "bot": true,
        "content": ["Ehh la verdad mi mayor fantasía..."]
      },
      {
        "bot": true,
        "content": ["Que prefieres, tratarme como una reina..."]
      }
    ],
    "max_delay": 60,
    "min_delay": 30,
    "user_kv_pairs": { "age": 30 },
    "conversation_id": "chat-57-10628047-21400194", 
    "degrade_grammar": 1.0,
    "enable_protections": true,
    "question_mode": null,
    "user_display_name": null,
    "bot_display_name": null
  })
});

// Response: Immediate completion or webhook
```

</div>

<div>

## V3 - Multi-Request Equivalent
```javascript
// Step 1: Create conversation (once)
const conversationResponse = await fetch('/api/conversations', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer sk_prod_abcd1234...',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    "bot_id": "88d86507-8d6c-4fad-b6f6-15d4fd377c83",
    "user_id": "306066b7-e47a-405b-8726-ccec362858ac",
    "create_user_if_not_exists": true,
    "webhook": "https://api.qkkie.com/webhook",
    "with_messages": [
      {
        "text": "Ehh la verdad mi mayor fantasía...",
        "from_bot": true
      },
      {
        "text": "Que prefieres, tratarme como una reina...",
        "from_bot": true
      }
    ]
  })
});

const { conversation } = await conversationResponse.json();

// Step 2: Send new message (for each message)
const messageResponse = await fetch(
  `/api/conversations/${conversation.id}/messages`, {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer sk_prod_abcd1234...',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    "message": {
      "text": "Hola",
      "from_bot": false,
      "attached_media": null
    }
  })
});

// Response: 202 Accepted, bot response via webhook
```

</div>

</div>