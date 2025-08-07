---

# V1 Segmentation vs V3 Atomic Messages

<style>
pre code { font-size: 8px !important; line-height: 1.0 !important; }
.compact-box h2 { margin: 0 !important; padding: 0 !important; }
.compact-box p { margin: 0 !important; }
.compact-box ul { margin: 0 !important; padding-left: 1rem !important; }
</style>

<div class="grid grid-cols-2 gap-4 text-xs">

<div>

**V1 message segmentation:** Messages as Arrays of Segments

```javascript
// V1 uses arrays of strings for messages
{
  "message": "Hello there!",
  "messages": [
    { "bot": true, "content": ["Hi! How are you doing today?", "I was just thinking about you.", "What are your plans for tonight?"] },
    { "bot": false, "content": ["Hey!", "I'm doing great, thanks for asking."] },
    { "bot": true, "content": ["That's wonderful to hear!", "I'm glad you're having a good day."] }
  ]
}
```

</div>

<div>

**V3 atomic messages**: 1 Message = 1 Text String, more standard pattern

```javascript
// V3 uses single text strings per message - just pass what the user sees!
{ "with_messages": [
    { "text": "Hi! How are you doing today?", "from_bot": true },
    { "text": "I was just thinking about you.", "from_bot": true },
    { "text": "What are your plans for tonight?", "from_bot": true },
    { "text": "Hey!", "from_bot": false },
    { "text": "I'm doing great, thanks for asking.", "from_bot": false },
    { "text": "That's wonderful to hear!", "from_bot": true },
    { "text": "I'm glad you're having a good day.", "from_bot": true }
  ]
}

```

</div>

</div>

<div class="mt-2 grid grid-cols-2 gap-4 text-xs">

<div class="compact-box p-2 bg-red-50 border-l-4 border-red-500 text-red-900">

**V1 Segmentation Complexity:**
- Bot responses arrays of strings
- Each segment represents a "part" of the message
- Delay between segments must be done on your side
- Impossible for the user to interrupt the bot between segments


</div>

<div class="compact-box p-2 bg-green-50 border-l-4 border-green-500 text-green-900">

**V3 Atomic Simplicity:**
- 1 message = 1 webhook payload = 1 atomic text string
- Bot and user can still send multiple messages, but simpler. No need to worry aboout segmentation on your end
- User can interrupt the bot mid segments

</div>

</div>

<div class="mt-2 p-2 bg-yellow-100 border-l-4 border-yellow-500 text-yellow-700 text-xs">
<strong>Migration Impact:</strong> Should become much simpler, but have to make sure you are handling strings instead of lists of strings on your end.
</div>