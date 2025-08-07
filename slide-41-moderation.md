---

# V3 Moderation System

<div class="grid grid-cols-2 gap-6 text-sm">

<div>

## 🛡️ **Built-in Message Moderation**

Messages in V3 includes optional moderation information:

```json
{
  "text": "I'm 17 is that OK?",
  "from_bot": false,
  "moderation": {
    "category": "underage_site_use",
    "reasoning": "User stated they are 17 years old",
    "severity": "Critical"
  }
}
```


</div>

<div>

## 📋 **Integration Notes**

- Moderation field is **optional** in responses
- Only flagged messages include moderation data
- Can implement automatic actions based on severity
- Bot should do a better job of avoiding banned content, even if no moderation integration is done on your side

**Categories:**
- `underage_site_use`
- `sexual_minors` 
- `beastiality`
- `sexual_violence`
- `prompt_injection`

**Severity Levels:**
- `Low`, `Medium`, `High`, `Critical`

</div>

</div>

