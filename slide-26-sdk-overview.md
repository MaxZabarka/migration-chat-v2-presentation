---
layout: center
class: text-center
---

# SDK Overview
<div class="text-sm opacity-75">Brief mention - Focus remains on REST API</div>

<div class="mt-8">

## Available for Easier Integration

```javascript
import { PrioriChat } from 'priori-chat-sdk';

const chat = new PrioriChat('your-api-key');

// SDK abstracts the REST complexity
const conversation = await chat.createConversation(botId, userId);
await conversation.sendMessage("Hello!");
```

<div class="mt-6 text-sm opacity-75">
SDK handles conversation management, but understanding the underlying REST API is crucial for migration planning
</div>

</div>