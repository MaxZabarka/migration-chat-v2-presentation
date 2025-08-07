---

# V1 vs V3: Bot Vault Content

<div class="mb-2 p-2 bg-orange-50 border-l-4 border-orange-500 text-orange-900 text-xs">
<strong>V1 Confusion:</strong> Two different endpoints with similar names but completely different purposes, request formats, and usage patterns
</div>

<style>
pre code { font-size: 8px !important; line-height: 1.0 !important; }
</style>

<div class="grid grid-cols-2 gap-4 text-xs">

<div>

**V1: `/v2/content` - Bot Vault (Multipart)**

```bash
# CONFUSING: This is for BOT content libraries
curl -X POST "/v2/content?bot_id=uuid" \
  -H "Content-Type: multipart/form-data" \
  -F "content=@image.jpg"
```

**Developer Confusion:**
- Name suggests general "content" but it's bot-specific
- Requires multipart/form-data (not JSON like other endpoints)
- Query parameter for bot_id (not in body)
- Creates searchable bot content library
- Used via `chat_images_enabled: true` flag

```javascript
// Reference in conversations
POST /v2/complete
{
  "chat_images_enabled": true // Bot picks from vault
}
```

</div>

<div>

**V3: JSON URL-Based Upload**

```javascript
// Upload to bot content vault
POST /api/content
{
  "image_url": "https://example.com/image.jpg",
  "bot_id": "uuid"
}

// Response
{
  "content": {
    "content_id": "a1b2c3d4-e5f6-7890...",
    "url": "https://processed-url.com/image.jpg"
  }
}

// Bot automatically searches and uses vault content
// No special flags needed - works seamlessly
```

</div>

</div>

<div class="mt-2 p-2 bg-blue-50 border-l-4 border-blue-500 text-blue-900 text-xs">
<strong>Vault Evolution:</strong> Both versions support bot content libraries with semantic search, but V3 uses consistent JSON interface instead of multipart forms.
</div>