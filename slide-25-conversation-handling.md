---

# Conversation Handling: V1 vs V3 

<div class="grid grid-cols-2 gap-4 text-sm">

<div>

## V1 - Stateless Pattern
```javascript
// V1 - Send full context every time
const sendMessage = async (conversationData) => {
  const response = await fetch('/v2/complete', {
    method: 'POST',
    headers: { 'Authorization': `Bearer ${token}` },
    body: JSON.stringify({
      conversation_id: conversationData.id,
      bot_id: conversationData.botId,
      user_id: conversationData.userId,
      message: conversationData.newMessage,
      messages: conversationData.fullHistory, // Full history each time
      webhook: conversationData.webhook,
      language: conversationData.language,
      platform: conversationData.platform,
      user_kv_pairs: conversationData.userContext
    })
  });
  
  return await response.json();
};

// Usage
await sendMessage({
  id: "chat-123",
  botId: "bot-456", 
  userId: "user-789",
  newMessage: "Hello",
  fullHistory: [
    { bot: true, content: ["Hi there!"] },
    { bot: false, content: ["Hey"] }
  ],
  webhook: "https://...",
  language: "es",
  platform: "Qkkie"
});
```

</div>

<div>

## V3 - Stateful Pattern
```javascript
// V3 - Server manages conversation state
class ConversationSession {
  constructor(token) {
    this.token = token;
    this.conversations = new Map();
  }

  async getOrCreateConversation(botId, userId, webhook) {
    const key = `${botId}-${userId}`;
    
    if (this.conversations.has(key)) {
      return this.conversations.get(key);
    }

    const response = await fetch('/api/conversations', {
      method: 'POST',
      headers: { 'Authorization': `Bearer ${this.token}` },
      body: JSON.stringify({
        bot_id: botId,
        user_id: userId,
        create_user_if_not_exists: true,
        webhook: webhook
      })
    });

    const conversation = await response.json();
    this.conversations.set(key, conversation.conversation);
    return conversation.conversation;
  }

  async sendMessage(conversationId, text) {
    return await fetch(`/api/conversations/${conversationId}/messages`, {
      method: 'POST',
      headers: { 'Authorization': `Bearer ${this.token}` },
      body: JSON.stringify({
        message: { text, from_bot: false }
      })
    });
  }
}
```

</div>

</div>

### V3 Session Management with Magic Move

````md magic-move {lines: true}
```javascript
// Step 1: Initialize session
const session = new ConversationSession(token);
```

```javascript
// Step 2: Get or create conversation  
const conversation = await session.getOrCreateConversation(
  "bot-456", 
  "user-789", 
  "https://webhook.example.com"
);
```

```javascript
// Step 3: Send message (no history needed - server remembers)
await session.sendMessage(conversation.id, "Hello");

// Server automatically maintains conversation state
// No need to send full message history each time
```
````