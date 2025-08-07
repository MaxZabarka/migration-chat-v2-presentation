---

# Code Migration: Bot Management Comparison

<div class="grid grid-cols-2 gap-4 text-sm">

<div>

## V1 Bot Management
```javascript
// V1 Bot Creation - Simple object format
const createBot = async (botData) => {
  const response = await fetch('/v2/bot', {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${token}`,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      name: botData.name,
      freeform_personality: botData.personality,
      kv_pairs: botData.attributes // Object format
    })
  });
  
  return await response.json();
};

// Usage
await createBot({
  name: "Angela",
  personality: "Friendly and outgoing",
  attributes: {
    age: "25",
    location: "NYC"
  }
});
```

**V1 Limitations:**
- Create only, no CRUD operations
- No way to list, update, or delete bots
- Object-based attributes

</div>

<div>

## V3 Bot Management  
```javascript
// V3 Bot Creation - Array format
const createBot = async (botData) => {
  const response = await fetch('/api/bots', {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${token}`,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      name: botData.name,
      freeform: botData.personality, // Renamed field
      attributes: Object.entries(botData.attributes).map(([name, value]) => ({
        name,
        value: String(value) // Must be strings
      }))
    })
  });
  
  return await response.json();
};

// Full CRUD Operations Available
await fetch(`/api/bots/${botId}`, { method: 'GET' });    // Read
await fetch(`/api/bots/${botId}`, { method: 'PUT', ... }); // Update  
await fetch(`/api/bots/${botId}`, { method: 'DELETE' });   // Delete
await fetch('/api/bots');                                  // List All
```

**V3 Advantages:**
- Full REST CRUD operations
- Array-based attributes for consistency
- Bot listing and management capabilities

</div>

</div>