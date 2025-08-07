---
layout: center
class: text-center
---

# SDK Overview

<div class="mt-8">

## Available for Easier Integration


```javascript
import { PrioriChat } from 'priori-chat-sdk';

const chat = new PrioriChat('your-api-key');

// SDK abstracts the REST complexity
const conversation = await chat.createConversation(botId, userId);
await conversation.sendMessage("Hello!");
```


</div>
