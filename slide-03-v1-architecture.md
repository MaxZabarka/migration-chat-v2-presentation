---

# V1 Architecture: Monolithic Action-Based

<div class="grid grid-cols-2 gap-6">

<div>

```mermaid {scale: 0.4}
graph TD
    A[Client] --> B[MONOLITH Complete Endpoint]
    A --> C[Bot Endpoint]  
    A --> D[Content Endpoint]
    A --> E[User Content Endpoint]
    
    B --> F[POST /v2/complete<br/>EVERYTHING in one call:<br/>bot_id + user_id + conversation_id<br/>+ message + webhook + messages<br/>+ language + platform + delays<br/>+ user_kv_pairs + protections<br/>+ images + user_content + etc.]
    F --> G[Bot Response<br/>Triggered by /complete calls]
    G --> H[Webhook<br/>Async message delivery]
    
    C -.-> I[POST /v2/bot<br/>Create bot with<br/>name + kv_pairs]
    D -.-> J[POST /v2/content<br/>Upload to bot vault]
    E -.-> K[POST /v2/user_content<br/>Upload for use in<br/>/v2/complete]
    
    style B fill:#e3f2fd,stroke:#1976d2,color:#000
    style C fill:#f3e5f5,stroke:#7b1fa2,color:#000
    style D fill:#f3e5f5,stroke:#7b1fa2,color:#000
    style E fill:#f3e5f5,stroke:#7b1fa2,color:#000
    style F fill:#fff3e0,stroke:#f57c00,color:#000
    style G fill:#e8f5e8,stroke:#2e7d2e,color:#000
    style H fill:#fff3e0,stroke:#f57c00,color:#000
```

</div>

<div>

**V1 Pattern - Action-Based:**
- `/v2/complete` - Add message + generate response in one call
- **Stateless conversations** - client manages conversation history
- **Action-oriented** - generating messages is triggered via `/v2/complete`
- Almost **everything passed to `/v2/complete`** - bot_id, user_id, conversation_id, webhook, messages, delays, etc.
- Webhook for async responses

</div>

</div>