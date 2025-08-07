---

# Adding a Message to Conversation

<div class="grid grid-cols-2 gap-6 text-sm">

<div>

## POST `/api/conversations/{id}/messages`

Adds a single message to an existing conversation. Triggers bot response via webhook.

**Key Features:**
- Atomic message format (`text` + `from_bot`)
- Optional media attachments
- `sent_at` support for temporal context
- Immediate webhook delivery
- Returns 202 Accepted for async processing

**Message Types:**
- User messages: `from_bot: false`
- Bot messages: `from_bot: true`
- Media support: `attached_media`
- `sent_at`: Informs bot of message timing

</div>

<div>

```json
POST /api/conversations/f47ac10b-58cc-4372-a567-0e02b2c3d479/messages
{
  "message": {
    "text": "You look absolutely stunning today 💕",
    "from_bot": false,
    "attached_media": null,
    "sent_at": 1705327800
  }
}
```

**With Media & sent_at:**
```json
{
  "message": {
    "text": "Sending you a special photo 😍",
    "from_bot": false,
    "sent_at": 1705327860,
    "attached_media": {
      "url": "https://example.com/photo.jpg",
      "type": "image"
    }
  }
}
```

💡 **sent_at (Unix time) helps bots understand:**
- Time of day context ("Good morning!")  
- Conversation pacing and delays
- Temporal references ("earlier today")

**Response:** `202 Accepted`
Bot response comes via webhook

</div>

</div>