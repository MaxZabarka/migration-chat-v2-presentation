---

# V1 vs V3: User Content & Profile Photos

<div class="mb-2 p-2 bg-orange-50 border-l-4 border-orange-500 text-orange-900 text-xs">
<strong>V1 Developer Confusion:</strong> `/v2/content` vs `/v2/user_content` - similar names, completely different implementations (multipart vs raw binary vs JSON)
</div>

<style>
pre code { font-size: 7px !important; line-height: 1.0 !important; }
</style>

<div class="grid grid-cols-2 gap-4 text-xs">

<div>

**V1: `/v2/user_content` - User Images (Raw Binary)**

```bash
# CONFUSING: This is for USER images, completely different!
curl -X POST "/v2/user_content" \
  -H "Content-Type: image/jpeg" \
  --data-binary "@photo.jpg"
# Response: {"id": "user-content-uuid"}
```

**More Developer Confusion:**
- Similar name to `/v2/content` but totally different purpose
- Raw binary body (not multipart, not JSON)
- No parameters needed (unlike /content)
- For user-sent images, not bot libraries
- Must reference by ID in separate API call

```javascript
// Step 2: Reference in /v2/complete (4+ different ways!)
POST /v2/complete
{
  "image_id": "user-content-uuid",    // Current message image
  "image_url": "https://direct.jpg",  // OR direct URL
  "user_images": ["profile-id-1"],    // OR profile photos
  "bot_images": ["bot-profile-id"]    // OR bot profiles
}
```

</div>

<div>

**V3: Direct Message Attachment**

```javascript
// Single step: attach directly to message
POST /api/conversations/conv-123/messages
{
  "message": {
    "text": "Here's my photo",
    "from_bot": false,
    "attached_media": {
      "url": "https://example.com/photo.jpg"
    }
  }
}

// Profile photos handled through user/bot objects
// Content processed on-demand
// No separate upload step required
```

**Benefits:**
- JSON-only, no binary uploads
- Single-step direct attachment
- One consistent way to handle content
- Profile photos managed at user/bot level

</div>

</div>

<div class="mt-2 grid grid-cols-2 gap-4 text-xs">

<div class="p-2 bg-red-50 border-l-4 border-red-500 text-red-900">
**V1 Confusion:** Similar endpoint names `/content` vs `/user_content` with completely different formats (multipart vs binary vs JSON) and purposes (bot vault vs user images)
</div>

<div class="p-2 bg-green-50 border-l-4 border-green-500 text-green-900">
**V3 Clarity:** Clear separation - `/api/content` for bot vault, `attached_media` in messages for user content. All JSON, consistent patterns.
</div>

</div>