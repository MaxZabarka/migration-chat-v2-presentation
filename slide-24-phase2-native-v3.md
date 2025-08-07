---

# Implementation Strategy: Phase 2 - Native V3

<div class="text-sm">

## Full V3 Implementation with Advanced Features

````md magic-move {lines: true}
```javascript
// Phase 2: Native V3 service (no V1 compatibility layer)
class ChatServiceV3 {
  constructor(token) {
    this.token = token;
    this.conversationCache = new Map();
  }

  async createConversation(botId, userId, webhook) {
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
    this.conversationCache.set(`${botId}-${userId}`, conversation);
    return conversation;
  }
}
```

```javascript
// Add core messaging functionality
class ChatServiceV3 {
  // ... constructor and createConversation ...

  async sendMessage(conversationId, text, attachedMedia = null) {
    return await fetch(`/api/conversations/${conversationId}/messages`, {
      method: 'POST',
      headers: { 'Authorization': `Bearer ${this.token}` },
      body: JSON.stringify({
        message: {
          text: text,
          from_bot: false,
          attached_media: attachedMedia
        }
      })
    });
  }

  async getConversationHistory(conversationId) {
    const response = await fetch(`/api/conversations/${conversationId}`, {
      headers: { 'Authorization': `Bearer ${this.token}` }
    });
    return await response.json();
  }
}
```

```javascript
// Add V3-exclusive advanced features
class ChatServiceV3 {
  // ... previous methods ...

  async getMemories(conversationId) {
    const response = await fetch(`/api/conversations/${conversationId}/memories`, {
      headers: { 'Authorization': `Bearer ${this.token}` }
    });
    return await response.json();
  }

  async uploadContent(botId, imageUrl) {
    return await fetch('/api/content', {
      method: 'POST',
      headers: { 'Authorization': `Bearer ${this.token}` },
      body: JSON.stringify({ bot_id: botId, image_url: imageUrl })
    });
  }

  async searchConversations(filters) {
    const params = new URLSearchParams(filters);
    return await fetch(`/api/conversations?${params}`, {
      headers: { 'Authorization': `Bearer ${this.token}` }
    });
  }

  async searchContent(botId, query, mediaType = null) {
    const params = new URLSearchParams({ bot_id: botId, search: query });
    if (mediaType) params.append('media_type', mediaType);
    
    return await fetch(`/api/content?${params}`, {
      headers: { 'Authorization': `Bearer ${this.token}` }
    });
  }
}
```
````

</div>