---

# V1 Request Structure Deep Dive

<div class="text-sm">

Real example from production system:

```javascript {all|3-4|5-6|7-17|18-23|24-29|30-35|all}
{
  // Core identifiers
  "bot_id": "88d86507-8d6c-4fad-b6f6-15d4fd377c83",
  "conversation_id": "chat-57-10628047-21400194",
  "user_id": "306066b7-e47a-405b-8726-ccec362858ac",
  "message": "Hola",

  // Conversation history (full context each time)
  "messages": [
    {
      "bot": true,
      "content": ["Ehh la verdad mi mayor fantasía es tener sexo anal..."]
    },
    {
      "bot": true, 
      "content": ["Que prefieres, tratarme como una reina delicada..."]
    }
  ],

  // Platform and localization
  "platform": "Qkkie",
  "language": "es", 
  "timezone": null,

  // Timing and behavior control
  "min_delay": 30,
  "max_delay": 60,
  "degrade_grammar": 1.0,
  "enable_protections": true,

  // User context and personalization  
  "user_kv_pairs": {"age": 30},
  "user_display_name": null,
  "bot_display_name": null,

  // Webhook for async responses
  "webhook": "https://api.qkkie.com/chat/clonetwin/messages?token=..."
}
```

</div>