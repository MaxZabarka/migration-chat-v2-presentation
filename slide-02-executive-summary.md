---
transition: fade-out
---

# Executive Summary

<v-clicks>

- **Architecture Shift**: Single endpoint `/v2/complete` → Multiple REST endpoints `/api/...`
- **State Management**: Stateless → Stateful conversations  
- **Message Flow**: Send full context each time → Create conversation once, add messages
- **Naming Clarification**: V1 API uses `/v2/complete`, V3 API uses `/api/...` routes

</v-clicks>

<div v-click class="mt-8 p-4 bg-red-100 border-l-4 border-red-500 text-red-700">
  <strong>Important:</strong> Some V1 features are not yet available in V3 - migration planning required
</div>