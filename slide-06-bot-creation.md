---

# Bot Creation Migration

<div class="grid grid-cols-2 gap-4 text-sm">

<div>

## V1 Bot Creation
```javascript
POST /v2/bot
{
  "name": "Angela",
  "freeform_personality": "Angela likes to talk about the weather and travel",
  "kv_pairs": {
    "age": "35",
    "residence": "Calgary", 
    "hair": "blonde",
    "body": "curvy"
  }
}
```

</div>

<div>

## V3 Bot Creation  
```javascript
POST /api/bots
{
  "name": "Angela",
  "freeform": "Angela likes to talk about the weather and travel", 
  "attributes": [
    {"name": "age", "value": "35"},
    {"name": "residence", "value": "Calgary"},
    {"name": "hair", "value": "blonde"},
    {"name": "body", "value": "curvy"}
  ]
}
```


</div>

</div>


<div class="mt-4 p-3 bg-blue-100 border-l-4 border-blue-500 text-blue-700 text-sm">
  <strong>Key Changes:</strong> <span class="bg-gray-200 text-gray-800 px-1 rounded">kv_pairs</span> object → <span class="bg-gray-200 text-gray-800 px-1 rounded">attributes</span> array </div>

<div class="mt-2 p-3 bg-green-100 border-l-4 border-green-500 text-green-700 text-sm">
  <strong>Migration Support:</strong> Existing bots can be migrated for you - contact us to transfer your V1 bots to V3 format
</div>