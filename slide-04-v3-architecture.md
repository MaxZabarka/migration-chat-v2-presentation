---

# V3 Architecture: Object-Oriented CRUD-Based

<div class="grid grid-cols-2 gap-6">

<div>

```mermaid {scale: 0.4}
graph TD
    A[Client] --> B[Bot Object<br/>POST /api/bots<br/>Contains: name, attributes,<br/>freeform, vault_images]
    A --> C[Conversation Object<br/>POST /api/conversations<br/>Contains: bot_id, user_id,<br/>webhook, messages]
    A --> D[Message Object<br/>POST /api/conversations/id/messages<br/>Contains: text, from_bot,<br/>attached_media]
    A --> E[User Object<br/>implicit creation<br/>Contains: profile_photos,<br/>attributes]
    A --> F[Content Object<br/>POST /api/content<br/>Contains: bot vault images,<br/>semantic search]
    
    D --> I[Bot Response<br/>Triggered by adding messages<br/>to conversation]
    I --> H[Webhook<br/>from conversation object]
    I --> J[Update State<br/>Messages added to<br/>conversation object]
    
    style B fill:#e8f5e8,stroke:#2e7d2e,color:#000
    style C fill:#e8f5e8,stroke:#2e7d2e,color:#000
    style D fill:#e8f5e8,stroke:#2e7d2e,color:#000
    style E fill:#e8f5e8,stroke:#2e7d2e,color:#000
    style F fill:#e8f5e8,stroke:#2e7d2e,color:#000
    style G fill:#ffebcd,stroke:#d2691e,color:#000
    style I fill:#e8f5e8,stroke:#2e7d2e,color:#000
    style H fill:#fff3e0,stroke:#f57c00,color:#000
    style J fill:#f0f8ff,stroke:#4682b4,color:#000
```

<div class="text-xs">

**V3 Pattern - CRUD-Based:**
- New endpoints: `/api/bots`, `/api/conversations`, `/api/messages`, `/api/users`, `/api/content`
- **Stateful conversations** - server manages conversation history
- **Resource-oriented** - generating bot messages is triggered by adding user messages

</div>

</div>

<div class="text-sm mt-30">

**Object Data Distribution:**
- **bot_id, user_id, webhook, delay, language, etc** → stored in **Conversation Object**
- **Unified content resource**. No more /user_content or /content confusion. you can represent all images either via url or unified id. Which can then be used in:
  - **images in conversation** → stored in **Message Objects** (attached_media)
  - **profile photos** → stored in respective **User/Bot Objects**
  - **secret photos** → stored in **Bot Object**

</div>

</div>