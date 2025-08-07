---

# Conversation Queries & Content

<div class="grid grid-cols-2 gap-6 text-xs">

<div>

## Query Conversations

**GET `/api/conversations`** - List conversations
```http
GET /api/conversations?bot_id=550e8400-e29b-41d4-a716-446655440000&user_id=user_123
```

**GET `/api/conversations/{id}`** - Get specific conversation with all messages
```http  
GET /api/conversations/f47ac10b-58cc-4372-a567-0e02b2c3d479
```

**PATCH `/api/conversations/{conversation_id}`** - Update webhook only
```json
{"webhook": "https://example.com/new-webhook"}
```

**GET `/api/conversations/{id}/memories`** - Get conversation memories

</div>

<div>

## Content Management

**GET `/api/content`** - List bot's media content
```http
GET /api/content?bot_id=550e8400&search=vacation&media_type=image
```

**POST `/api/content`** - Upload new media
```json
{
  "bot_id": "550e8400-e29b-41d4-a716-446655440000",
  "image_url": "https://example.com/sexy-photo.jpg"
}
```

**DELETE `/api/content/{content_id}`** - Delete media

## API Keys

**GET `/api/api-keys`** - List your API keys

**POST `/api/api-keys`** - Create new API key

</div>

</div>

<div class="mt-4 p-3 bg-yellow-50 border-l-4 border-yellow-500 text-yellow-700 text-xs">
<strong>Migration Tip:</strong> Use <code>GET /api/conversations?bot_id=X&user_id=Y</code> to check if conversation exists before creating new ones.
</div>