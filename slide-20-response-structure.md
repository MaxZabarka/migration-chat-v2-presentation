---

# Response Structure: V1 vs V3

<div class="grid grid-cols-2 gap-4 text-sm">

<div>

## V1 Response - Immediate Completion
```javascript
// V1 /v2/complete response
{
  "response": "¡Hola! ¿Cómo estás? Me alegra que me escribas 😊",
  "conversation_id": "chat-57-10628047-21400194",
  "bot_id": "88d86507-8d6c-4fad-b6f6-15d4fd377c83",
  "message_id": "msg_987654",
  "delay": 45, // Actual delay used
  "tone": "friendly",
  "moderation": null,
  "timestamp": 1640995205
}
```

**V1 Response Pattern:**
- Immediate synchronous response
- Contains generated message
- Includes timing information
- Simple, flat structure

</div>

<div>

## V3 Response - Async Acknowledgment
```javascript
// V3 POST /api/conversations/{id}/messages response
// Status: 202 Accepted
{
  // Empty body - processing async
}

// Actual response comes via webhook:
{
  "event": "message.created",
  "conversation_id": "conv_abc123", 
  "bot_id": "88d86507-8d6c-4fad-b6f6-15d4fd377c83",
  "user_id": "306066b7-e47a-405b-8726-ccec362858ac",
  "message": {
    "id": "msg_xyz789",
    "text": "¡Hola! ¿Cómo estás? Me alegra que me escribas 😊",
    "from_bot": true,
    "sent_at": 1640995205,
    "message_tone": "Friendly",
    "moderation": {
      "category": null,
      "severity": "Low"
    },
    "attached_media": null
  },
  "conversation_messages_count": 4
}
```

**V3 Response Pattern:**
- Async acknowledgment (202)
- Rich webhook payload
- Detailed message metadata
- Conversation context included

</div>

</div>