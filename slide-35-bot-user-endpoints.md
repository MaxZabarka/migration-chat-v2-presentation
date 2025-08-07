---

# Bot Management

<div class="text-sm">

## Bot Endpoints

**POST `/api/bots`** - Create new bot
```json
{
  "name": "Scarlett",
  "freeform": "Scarlett loves to travel, she is fresh out of college. Her personality is shy but flirty.",
  "attributes": [
    {"name": "age", "value": "23"},
    {"name": "residence", "value": "New York"},
    {"name": "height", "value": "five foot two inches"},
    {"name": "hair", "value": "long, wavy, blonde"},
    {"name": "orientation", "value": "bisexual"}
  ]
}
```

**GET `/api/bots/{id}`** - Get bot details

**PUT `/api/bots/{id}`** - Update bot (full update)

**DELETE `/api/bots/{id}`** - Delete bot


</div>
