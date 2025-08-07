---

# V1 vs V3 Request Structure Comparison

<div class="grid grid-cols-2 gap-4 text-xs">

<div>

## V1 - Everything in One Request
```javascript
POST /v2/complete
{
  "bot_id": "88d86507-8d6c-4fad-b6f6-15d4fd377c83",
  "conversation_id": "chat-57-10628047-21400194", 
  "user_id": "306066b7-e47a-405b-8726-ccec362858ac",
  "message": "Hola",
  "messages": [...], // Full conversation history
  "platform": "Qkkie",
  "language": "es", 
  "timezone": "Europe/Madrid",
  "min_delay": 30,
  "max_delay": 60,
  "degrade_grammar": 1.0,
  "user_kv_pairs": {"age": 30},
  "user_display_name": "Max",
  "bot_display_name": "Angela",
  "enable_protections": true,
  "question_mode": "enabled",
  "webhook": "https://api.qkkie.com/webhook"
}
```

**V1 Pattern:**
- Single request with full context
- Rich metadata and personalization
- Platform and language awareness
- Timing and behavior controls

</div>

<div>

## V3 - Split into Multiple Requests

**Step 1: Create Conversation**
```javascript
POST /api/conversations
{
  "bot_id": "88d86507-8d6c-4fad-b6f6-15d4fd377c83",
  "user_id": "306066b7-e47a-405b-8726-ccec362858ac",
  "create_user_if_not_exists": true,
  "webhook": "https://api.qkkie.com/webhook",
  "with_messages": [
    {
      "text": "Previous message...",
      "from_bot": true
    }
  ]
}
```

**Step 2: Send Message**
```javascript
POST /api/conversations/conv_abc123/messages
{
  "message": {
    "text": "Hola",
    "from_bot": false,
    "attached_media": null
  }
}
```

**V3 Pattern:**
- Multi-step workflow
- Server-side state management
- ❌ **Missing**: platform, language, timezone
- ❌ **Missing**: timing controls, user context

</div>

</div>