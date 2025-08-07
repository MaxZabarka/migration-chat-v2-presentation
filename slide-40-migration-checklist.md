---

# Summary: Migration Checklist

<div class="grid grid-cols-2 gap-6 text-sm">

<div>

## ✅ **Core Changes**

### 1. Base URL Update
- ❌ `dev-api.prioros.com/v2/` 
- ✅ `dev-api.prioros.com/v3/api/`
- 🚧 **Currently staging environment only**

### 2. Use New `/api/messages` Endpoint
- Replace `/v2/complete` with `/api/messages`

### 3. Update User Identification
- Change from `conversation_id`  to `user_id` 
- Use `create_user_if_not_exists: true` and `with_messages` for seamless data migration

</div>

<div>

## 🔄 **Data Format Changes**

### 4. Update Message Format
- Convert segmented messages to atomic messages
- Change `bot` → `from_bot`
- Change `content` array → `text` string
- See message format slide for examples

### 5. Update Webhook Handler
- New payload structure with `conversation_id` + `message` 
- Single message per webhook (no more segmented arrays)
- See webhook payload slide for comparison

</div>

</div>

<div class="mt-4 p-4 bg-green-50 border-l-4 border-green-500 text-green-800 text-sm">
<strong>🚀 Ready to migrate?</strong> Start with staging environment and follow the checklist above.
</div>
