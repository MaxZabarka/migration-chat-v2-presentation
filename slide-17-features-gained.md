---

# Features Gained in V3

<div class="grid grid-cols-2 gap-6">

<div>

## 🗄️ Persistent Storage
<div class="text-sm">

```javascript
// Conversations stored server-side
GET /api/conversations/conv_123
// Returns full message history

// No need to send full context each time
POST /api/conversations/conv_123/messages
```

</div>

## 🧠 Memory System
<div class="text-sm">

```javascript
GET /api/conversations/conv_123/memories
{
  "bot_memories": ["User likes pizza"],
  "user_memories": ["Bot is from NYC"]  
}
```

</div>

## 📁 Content Management
<div class="text-sm">

```javascript
POST /api/content
{
  "bot_id": "bot_123",
  "image_url": "https://example.com/pic.jpg"
}

GET /api/content?search=vacation&media_type=image
```

</div>

</div>

<div>

## 🔍 Advanced Querying
<div class="text-sm">

```javascript
GET /api/conversations?min_messages=5
  &message_content=vacation
  &min_last_message_date=1640995200
```

</div>

## 📊 Rich Metadata
<div class="text-sm">

```javascript
{
  "text": "Hello!",
  "sent_at": 1640995200,
  "message_tone": "Friendly", 
  "moderation": {
    "category": "safe",
    "severity": "Low"
  }
}
```

</div>

## 🔑 API Key Management
<div class="text-sm">

```javascript
POST /api/api-keys {"name": "Production"}
GET /api/api-keys
DELETE /api/api-keys/{key_id}
```

</div>

</div>

</div>