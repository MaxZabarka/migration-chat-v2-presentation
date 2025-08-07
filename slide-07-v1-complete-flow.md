---
layout: two-cols
layoutClass: gap-8
---

# Message Generation: V1 Complete Flow

::left::

<div class="text-sm">

**Single Request Pattern**
```javascript
POST /v2/complete
{
  "conversation_id": "chat-57-10628047-21400194",
  "bot_id": "88d86507-8d6c-4fad-b6f6-15d4fd377c83",
  "message": "Hola",
  "messages": [
    {
      "bot": true,
      "content": ["Hey sexy, what's up?"]
    },
    {
      "bot": false, 
      "content": ["not much, you?"]
    }
  ],
  "user_id": "306066b7-e47a-405b-8726-ccec362858ac",
  "webhook": "https://api.example.com/webhook",
  "language": "es",
  "platform": "Qkkie",
  "user_kv_pairs": {"age": 30}
}
```

</div>

::right::

<div class="text-sm">

**Response & Characteristics**
- 🔄 **Stateless**: Full conversation sent each time
- ⚡ **Immediate**: Synchronous completion 
- 🌍 **Rich Context**: Language, platform, user data
- ⏱️ **Timing Control**: min_delay, max_delay
- 🎭 **Personality**: Grammar degradation, tone control
- 📱 **Platform-Aware**: Tinder, Qkkie, etc.

</div>

<div v-click class="mt-4 p-3 bg-yellow-100 border-l-4 border-yellow-500 text-yellow-700 text-sm">
  <strong>Note:</strong> Many of these features are not available in V3 yet
</div>