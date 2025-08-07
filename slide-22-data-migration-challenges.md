---

# Data Migration Challenges

<div class="grid grid-cols-2 gap-6">

<div>

## 📊 Conversation History
<div class="text-sm">

```javascript
// V1 - Client manages history
const conversationHistory = [
  {bot: true, content: ["Hello"]},
  {bot: false, content: ["Hi"]},
  {bot: true, content: ["How are you?"]}
];

// Send with each request
fetch('/v2/complete', {
  body: JSON.stringify({
    messages: conversationHistory,
    message: "I'm good, thanks!"
  })
});
```

</div>

## 👤 User Profile Data
<div class="text-sm">

```javascript
// V1 - Rich user context
{
  "user_kv_pairs": {
    "age": 30,
    "location": "NYC", 
    "interests": "travel,food"
  },
  "user_freeform": "Looking for casual dating",
  "user_display_name": "Max"
}

// V3 - Only user_id
{
  "user_id": "306066b7-e47a-405b-8726-ccec362858ac"
}
```

</div>

</div>

<div>

## 🔄 Migration Strategy
<div class="text-sm">

```javascript
// Data transformation needed
function migrateToV3(v1Request) {
  // 1. Create bot if not exists
  const bot = await createBot(v1Request.bot_id);
  
  // 2. Create conversation with history
  const conversation = await createConversation({
    bot_id: bot.id,
    user_id: v1Request.user_id,
    with_messages: v1Request.messages.map(msg => ({
      text: msg.content[0],
      from_bot: msg.bot
    }))
  });
  
  // 3. Send new message
  await sendMessage(conversation.id, v1Request.message);
  
  // 4. Store missing context externally
  await storeUserContext(v1Request.user_id, {
    platform: v1Request.platform,
    language: v1Request.language,
    user_kv_pairs: v1Request.user_kv_pairs
  });
}
```

</div>

</div>

</div>