---

# Implementation Strategy: Phase 1 - Dual Support

<div class="text-sm">

## Gradual Migration with Fallback Strategy

````md magic-move {lines: true}
```javascript
// Current V1 implementation
class ChatService {
  async generateMessage(request) {
    return await fetch('/v2/complete', {
      method: 'POST',
      headers: { 'Authorization': `Bearer ${this.token}` },
      body: JSON.stringify(request)
    });
  }
}
```

```javascript
// Phase 1: Add V3 support with V1 fallback
class ChatService {
  constructor(apiVersion = 'v1') {
    this.apiVersion = apiVersion;
  }

  async generateMessage(request) {
    if (this.apiVersion === 'v3') {
      try {
        return await this.generateV3Message(request);
      } catch (error) {
        console.warn('V3 failed, falling back to V1:', error);
        return await this.generateV1Message(request);
      }
    }
    return await this.generateV1Message(request);
  }

  async generateV1Message(request) {
    return await fetch('/v2/complete', {
      method: 'POST', 
      headers: { 'Authorization': `Bearer ${this.token}` },
      body: JSON.stringify(request)
    });
  }
}
```

```javascript
// Phase 1: V3 implementation with V1 request transformation
class ChatService {
  async generateV3Message(v1Request) {
    // 1. Get or create conversation
    let conversation = await this.findConversation(
      v1Request.bot_id, 
      v1Request.user_id
    );
    
    if (!conversation) {
      conversation = await fetch('/api/conversations', {
        method: 'POST',
        headers: { 'Authorization': `Bearer ${this.token}` },
        body: JSON.stringify({
          bot_id: v1Request.bot_id,
          user_id: v1Request.user_id,
          webhook: v1Request.webhook,
          with_messages: this.transformMessages(v1Request.messages)
        })
      }).then(r => r.json());
    }

    // 2. Send message
    await fetch(`/api/conversations/${conversation.id}/messages`, {
      method: 'POST',
      headers: { 'Authorization': `Bearer ${this.token}` },
      body: JSON.stringify({
        message: { text: v1Request.message, from_bot: false }
      })
    });

    return { status: 'accepted', conversation_id: conversation.id };
  }

  transformMessages(v1Messages) {
    return v1Messages.map(msg => ({
      text: msg.content[0],
      from_bot: msg.bot
    }));
  }
}
```
````

</div>