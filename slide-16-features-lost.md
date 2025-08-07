---
layout: two-cols
layoutClass: gap-8
---

# Features Lost in V3 Migration

::left::

## Context & Localization
<div class="text-sm">

```javascript
// V1 Only - Not available in V3
{
  "language": "es",           // ❌ Lost
  "platform": "Qkkie",       // ❌ Lost  
  "timezone": "Europe/Madrid" // ❌ Lost
}
```

</div>

## Timing & Behavior
<div class="text-sm">

```javascript
// V1 Only
{
  "min_delay": 30,           // ❌ Lost
  "max_delay": 60,           // ❌ Lost
  "degrade_grammar": 1.0,    // ❌ Lost  
  "fast_mode": true          // ❌ Lost
}
```

</div>

## User Personalization  
<div class="text-sm">

```javascript
// V1 Only
{
  "user_kv_pairs": {"age": 30},     // ❌ Lost
  "user_freeform": "Looking for...", // ❌ Lost
  "user_display_name": "Max",       // ❌ Lost
  "bot_display_name": "Angela"      // ❌ Lost
}
```

</div>

::right::

## Media Handling
<div class="text-sm">

```javascript
// V1 Only
{
  "image_id": "img_123",           // ❌ Lost
  "image_url": "https://...",      // ❌ Lost
  "user_images": [...],           // ❌ Lost
  "bot_images": [...],            // ❌ Lost
  "chat_images_enabled": true     // ❌ Lost
}
```

</div>

## Protection & Control
<div class="text-sm">

```javascript
// V1 Only  
{
  "enable_protections": true,      // ❌ Lost
  "question_mode": "enabled",      // ❌ Lost
  "follow_up": null,              // ❌ Lost
  "is_follow_up": false           // ❌ Lost
}
```

</div>

<div class="mt-4 p-3 bg-red-100 border-l-4 border-red-500 text-red-700 text-sm">
  <strong>Critical:</strong> These features need alternative solutions or roadmap planning
</div>