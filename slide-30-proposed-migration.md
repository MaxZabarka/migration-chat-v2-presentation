---

# Proposed Migration: V1 to V3 Transformation

<div class="text-sm slide-30-small-code">


````md magic-move {lines: true}
```python {*}{maxHeight:'300px'}{class:'!children:text-xs'}
# Step 1: Original V1 approach
def send_message(conversation_id, bot_id, message):
    requests.post('/v2/complete', json={
        "conversation_id": conversation_id, "bot_id": bot_id,
        "message": message, "webhook": "https://api.example.com/webhook"
    })
    # Response will come via webhook
```

```python {*}{maxHeight:'300px'}{class:'!children:text-xs'}
# Step 2: Switch to V3 message endpoint
def send_message(user_id, bot_id, message):
    requests.post('/api/conversations/{conversation_id}/messages', json={
        "message": {"text": message, "from_bot": False}
    })
    # Response will come via webhook
```

```python {*}{maxHeight:'300px'}{class:'!children:text-xs'}
# Step 3: Conversation must be created first!
def send_message(user_id, bot_id, message):
    # Create conversation first
    conv_response = requests.post('/api/conversations', json={
        "bot_id": bot_id, "user_id": user_id,
        "create_user_if_not_exists": True,  # ← Seamless user creation
        "webhook": "https://api.example.com/webhook"
    })
    conversation_id = conv_response.json()["conversation"]["id"]
    # Then send message
    requests.post(f'/api/conversations/{conversation_id}/messages', json={
        "message": {"text": message, "from_bot": False}
    })
    # Response will come via webhook
```

```python {*}{maxHeight:'300px'}{class:'!children:text-xs'}
# Step 4: Optionally add bot messages after creation, like a start message
def send_message(user_id, bot_id, message):
    # Create conversation
    conv_response = requests.post('/api/conversations', json={
        "bot_id": bot_id,
        "user_id": user_id,
        "create_user_if_not_exists": True,
        "webhook": "https://api.example.com/webhook"
    })
    conversation_id = conv_response.json()["conversation"]["id"]
    
    # Add initial bot message with image
    requests.post(f'/api/conversations/{conversation_id}/messages', json={
        "message": {
            "text": "Hello",
            "from_bot": True,
            "attached_media": {"url": "https://example.com/start-image.jpg"}
        }
    })
    
    # Send user message
    requests.post(f'/api/conversations/{conversation_id}/messages', json={
        "message": {"text": message, "from_bot": False}
    })
    # Response will come via webhook
```

```python {*}{maxHeight:'300px'}{class:'!children:text-xs'}
# Step 5: Use with_messages for initial bot message (more efficient)
def send_message(user_id, bot_id, message):
    # Create conversation with initial bot message
    conv_response = requests.post('/api/conversations', json={
        "bot_id": bot_id,
        "user_id": user_id,
        "create_user_if_not_exists": True,
        "webhook": "https://api.example.com/webhook",
        "with_messages": [{
            "text": "Hey! Check out this photo 📸",
            "from_bot": True,
            "attached_media": {"url": "https://example.com/start-image.jpg"}
        }]
    })
    conversation_id = conv_response.json()["conversation"]["id"]
    
    # Send user message
    requests.post(f'/api/conversations/{conversation_id}/messages', json={
        "message": {"text": message, "from_bot": False}
    })
    # Response will come via webhook
```

```python {*}{maxHeight:'300px'}{class:'!children:text-xs'}
# Step 6: Check for existing conversation first
def send_message(user_id, bot_id, message):
    # Check if conversation already exists
    existing = requests.get('/api/conversations', params={
        "bot_id": bot_id, "user_id": user_id
    })
    
    if existing.json()["conversations"]:
        conversation_id = existing.json()["conversations"][0]["id"]
    else:
        # Create new conversation with initial bot message
        conv_response = requests.post('/api/conversations', json={
            "bot_id": bot_id,
            "user_id": user_id,
            "create_user_if_not_exists": True,
            "webhook": "https://api.example.com/webhook",
            "with_messages": [{
                "text": "Hello!",
                "from_bot": True,
                "attached_media": {"url": "https://example.com/start-image.jpg"}
            }]
        })
        conversation_id = conv_response.json()["conversation"]["id"]
    
    # Send user message
    requests.post(f'/api/conversations/{conversation_id}/messages', json={
        "message": {"text": message, "from_bot": False}
    })
    # Response will come via webhook
```

```python {*}{maxHeight:'300px'}{class:'!children:text-xs'}
# Step 7: Final solution - handle existing messages parameter
def send_message(message, user_id, bot_id, existing_messages=None):
    # Check if conversation already exists
    existing = requests.get('/api/conversations', params={
        "bot_id": bot_id, "user_id": user_id
    })
    
    if existing.json()["conversations"]:
        conversation_id = existing.json()["conversations"][0]["id"]
    elif existing_messages:
        # Create conversation with existing message history
        conv_response = requests.post('/api/conversations', json={
            "bot_id": bot_id,
            "user_id": user_id,
            "create_user_if_not_exists": True,
            "webhook": "https://api.example.com/webhook",
            "with_messages": initial_messages
        })
        conversation_id = conv_response.json()["conversation"]["id"]
    else:
        # Create conversation with a start message
        conv_response = requests.post('/api/conversations', json={
            "bot_id": bot_id,
            "user_id": user_id,
            "create_user_if_not_exists": True,
            "webhook": "https://api.example.com/webhook",
            "with_messages": [{
                "text": "Hey!",
                "from_bot": True,
                "attached_media": {"url": "https://example.com/start-image.jpg"}
            }]
        })
        conversation_id = conv_response.json()["conversation"]["id"]
    
    # Send user message
    requests.post(f'/api/conversations/{conversation_id}/messages', json={
        "message": {"text": message, "from_bot": False}
    })
    
    # Response will come via webhook (202 Accepted)
```
````

</div>
