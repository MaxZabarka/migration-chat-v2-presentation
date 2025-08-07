---
theme: seriph
background: https://cover.sli.dev
title: Chat API Migration Guide
info: |
  ## Chat API Migration Guide
class: text-center text-sm
drawings:
  persist: false
transition: slide-left
mdc: true
headings: 
  level: small
---

<style>
h1 { @apply text-xl !important; }
h2 { @apply text-lg !important; }
h3 { @apply text-base !important; }
h4 { @apply text-sm !important; }
.slidev-layout h1 { @apply text-2xl !important; }
.slidev-layout h2 { @apply text-lg !important; }
.slidev-layout h3 { @apply text-base !important; }

/* Slide 30 specific styles for smaller code */
.slide-30-small-code .slidev-code {
  font-size: 12px !important;
  line-height: 1.3 !important;
}

/* Slide 34 specific styles for smaller code */
.slide-34-small-code .slidev-code {
  font-size: 8px !important;
  line-height: 1.2 !important;
}

/* Slide 34 smaller h2 */
.slide-34-small-code h2 {
  font-size: 1rem !important;
}
</style>

# Chat API Migration Guide


<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub" title="Open in GitHub" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:logo-github />
  </a>
</div>


---
src: ./slide-02-executive-summary.md
---

---
src: ./slide-31-create-conversation.md
---

---
src: ./slide-32-add-message.md
---

---
src: ./slide-33-retrieve-conversation.md
---


---
src: ./slide-09-v1-flow-demo.md
---

---
src: ./slide-10-v3-flow-demo.md
---

---
src: ./slide-34-smart-add-message.md
---

---
src: ./slide-35-bot-user-endpoints.md
---

---
src: ./slide-06-bot-creation.md
---

---
src: ./slide-36-conversation-queries.md
---

---
src: ./slide-05-authentication.md
---

---
src: ./slide-11-segmentation-comparison.md
---

---
src: ./slide-04-v3-architecture.md
---

---
src: ./slide-03-v1-architecture.md
---


---
src: ./slide-41-moderation.md
---


---
src: ./slide-30-proposed-migration.md
---


---
src: ./slide-26-sdk-overview.md
---


---
src: ./slide-37-endpoint-comparison.md
---

---
src: ./slide-38-webhook-payload-changes.md
---

---
src: ./slide-39-message-format-changes.md
---

---
src: ./slide-40-migration-checklist.md
---

---
src: ./slide-27-migration-timeline.md
---

---
src: ./slide-29-thank-you.md
---

