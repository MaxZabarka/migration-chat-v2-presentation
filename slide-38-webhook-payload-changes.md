---

# Summary: Webhook Payload Changes

<div class="grid grid-cols-2 gap-6 text-sm">

<div>

## V1 Webhook Payload

```json
{
  "completion": [
    "Hey there! Can't wait to see you tonight 😍",
    "What do you want to do together?"
  ],
  "id": "b2c3d4e5-f6a7-8901-bcde-f23456789012",
  "media": {
    "url": "https://example.com/flirty-pic.jpg",
    "type": "image"
  },
  "media_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
}
```

**Format:**
- `completion`: Array of message segments
- `id`: Message ID
- `media`/`media_id`: Separate media fields

</div>

<div>

## V3 Webhook Payload

```json
{
  "conversation_id": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
  "message": {
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "text": "Hey there! Can't wait to see you tonight 😍",
    "from_bot": true,
    "sent_at": 1705327920,
    "attached_media": {
      "url": "https://example.com/flirty-pic.jpg",
      "content_id": "b2c3d4e5-f6a7-8901-bcde-f23456789012"
    }
  }
}
```

**Format:**
- `conversation_id`: Identifies the conversation
- `message`: Single atomic message object
- `sent_at`: Unix timestamp
- `attached_media`: Structured media object

</div>

</div>

<div class="mt-4 p-3 bg-red-50 border-l-4 border-red-500 text-red-800 text-xs">
<strong>⚠️ Breaking Change:</strong> Your webhook handler must be updated to handle the new payload structure. Single message per webhook instead of segmented arrays.
</div>