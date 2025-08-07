---

# Message Generation: V1 Single Request Flow

<div class="grid grid-cols-2 gap-6 text-sm">

<div>

## V1 Complete Request
```javascript
POST /v2/complete
{
  "bot_id": "88d86507-8d6c-4fad-b6f6-15d4fd377c83",
  "user_id": "306066b7-e47a-405b-8726-ccec362858ac",
  "conversation_id": "chat-123",
  "message": "Hola",
  "messages": [
    {
      "bot": true,
      "content": ["Hey there!"]
    }
  ],
  "webhook": "https://api.example.com/webhook",
  "language": "es",
  "platform": "Qkkie",
  "min_delay": 30,
  "max_delay": 60,
  "user_kv_pairs": {"age": 25}
}
```

</div>

<div>

## V1 Characteristics
- **🔥 Single endpoint** - everything in one request
- **📦 Stateless** - full context sent each time
- **⚡ Rich context** - language, platform, timing, user data
- **🎯 Direct response** - immediate or webhook
- **🛠️ Full feature set** - all parameters available

</div>

</div>