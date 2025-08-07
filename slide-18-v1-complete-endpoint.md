---

# V1 Complete Endpoint - Everything in One Request

<div class="text-sm">

The `/v2/complete` endpoint required **all context** to generate a response:

```javascript
POST /v2/complete
{
  // Required identifiers
  "bot_id": "88d86507-8d6c-4fad-b6f6-15d4fd377c83",      // Which bot personality
  "user_id": "306066b7-e47a-405b-8726-ccec362858ac",     // Which user is messaging
  "conversation_id": "chat-57-10628047-21400194",        // Conversation thread ID
  "message": "Hola",                                      // New message to respond to

  // Complete conversation history (sent every time)
  "messages": [
    {"bot": true, "content": ["Previous bot message 1"]},
    {"bot": false, "content": ["Previous user message"]},
    {"bot": true, "content": ["Previous bot message 2"]}
  ],

  // Response delivery
  "webhook": "https://api.example.com/webhook",           // Where to send bot response

  // Generation behavior controls
  "platform": "Qkkie",                                   // Dating platform context  
  "language": "es",                                       // Response language
  "min_delay": 30,                                       // Minimum response delay
  "max_delay": 60,                                       // Maximum response delay
  "degrade_grammar": 1.0,                                // Grammar imperfection level
  "enable_protections": true,                            // Safety controls

  // User personalization context
  "user_kv_pairs": {"age": 30, "location": "NYC"},      // User attributes
  "user_display_name": "Max",                           // User's display name
  "bot_display_name": "Angela",                         // Bot's display name
  "timezone": "America/New_York"                        // User timezone
}
```

**V1 Pattern**: Every request contained **complete context** - identifiers, full conversation history, generation settings, and delivery instructions.

</div>