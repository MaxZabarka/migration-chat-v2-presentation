---
layout: default
---

# Proposed Migration: V1 to V3 Transformation

<div class="text-sm slide-30-small-code text-left">


````md magic-move {lines: true}
```python {all|5|6|7}{*}{maxHeight:'300px'}{class:'!children:text-xs'}
# Step 1: Your current V1 implementation
def send_message(conversation_id, bot_id, message, message_history):
    # Uses conversation_id to identify existing chats
    # Messages format: {"bot": true, "content": [
    #   "Hi there! 👋",           ← First segment
    #   "How are you today?",     ← Second segment  
    #   "What's on your mind?"    ← Third segment
    # ]} (segmented)
    
    requests.post('/v2/complete', json={
        "conversation_id": conversation_id,
        "bot_id": bot_id,
        "message": message,
        "messages": message_history,
        "webhook": "https://api.example.com/webhook"
    })
    # Response will come via webhook
```

```python {all|6-9|11-21|22-26}{*}{maxHeight:'300px'}{class:'!children:text-xs'}
# Step 2: Migrating to V3 REST architecture
def send_message(user_id, bot_id, message, message_history):
    # Now uses user_id instead of conversation_id for identification
    # Messages format: {"text": "Hi!", "from_bot": true} (atomic)
    
    # Check if conversation exists
    existing = requests.get('/api/conversations', params={
        "bot_id": bot_id, "user_id": user_id
    })
    
    if existing.json()["conversations"]:
        conversation_id = existing.json()["conversations"][0]["id"]
    else:
        # Create conversation first
        conv_response = requests.post('/api/conversations', json={
            "bot_id": bot_id, "user_id": user_id,
            "create_user_if_not_exists": True,
            "webhook": "https://api.example.com/webhook",
            "with_messages": message_history
        })
        conversation_id = conv_response.json()["conversation"]["id"]
    
    # Then send message
    requests.post(f'/api/conversations/{conversation_id}/messages', json={
        "message": {"text": message, "from_bot": False}
    })
    # Response will come via webhook
```

```python {all|8|9-15}{*}{maxHeight:'300px'}{class:'!children:text-xs'}
# Step 3: Simplified with new /api/messages endpoint  
def send_message(user_id, bot_id, message, message_history):
    # Back to single call - handles conversation lookup/creation automatically
    # Still uses user_id identification and atomic message format
    # with_messages brings existing conversation history when creating new conversations
    
    requests.post('/api/messages', json={
        "message": {"text": message, "from_bot": False},
        "conversation_creation_params": {
            "bot_id": bot_id,
            "user_id": user_id,
            "create_user_if_not_exists": True,
            "webhook": "https://api.example.com/webhook",
            "with_messages": message_history  # Bring existing conversation history
        }
    })
    # Response will come via webhook
```

```python {*}{maxHeight:'300px'}{class:'!children:text-xs'}
# Step 4: Add initial messages for new conversations
def send_message(user_id, bot_id, message):
    # with_messages can also be used to add initial bot messages for new conversations
    # Perfect for conversation starters
    
    requests.post('/api/messages', json={
        "message": {"text": message, "from_bot": False},
        "conversation_creation_params": {
            "bot_id": bot_id,
            "user_id": user_id,
            "create_user_if_not_exists": True,
            "webhook": "https://api.example.com/webhook",
            "with_messages": [{
                "text": "Hey! Welcome to the chat 👋",
                "from_bot": True
            }]  # Initial greeting message
        }
    })
    # Response will come via webhook
```

````

</div>
