---

# Summary: Message Format Changes

<div class="grid grid-cols-2 gap-6 text-sm">

<div>

## V1: Segmented Messages

```json
{ "messages": [ {
      "bot": true,
      "content": [
        "Hey gorgeous! 💕", "How was your day?", "I've been thinking about you"
      ]
    },
    {
      "bot": false,
      "content": [
        "Aww you're so sweet!", "My day was good"
      ]
    }
  ]
}
```

**Characteristics:**
- Multiple segments per message
- `bot` boolean field
- `content` array of strings

</div>

<div>

## V3: Atomic Messages

```json
{
  "with_messages": [
    {"text": "Hey gorgeous! 💕", "from_bot": true},
    {"text": "How was your day?", "from_bot": true},  
    {"text": "I've been thinking about you", "from_bot": true},
    {"text": "Aww you're so sweet!", "from_bot": false},
    {"text": "My day was good", "from_bot": false}
  ]
}
```

**Characteristics:**
- One message = one text string
- `from_bot` boolean field  
- `text` single string
- Optional `attached_media`

</div>

</div>

<div class="mt-4 p-3 bg-yellow-50 border-l-4 border-yellow-500 text-yellow-800 text-xs">
<strong>Migration Impact:</strong> You must convert segmented messages to individual atomic messages. Each segment becomes a separate message object.
</div>
