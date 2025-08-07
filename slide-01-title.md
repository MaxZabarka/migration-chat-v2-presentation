---
theme: seriph
background: https://cover.sli.dev
title: Chat API Migration Guide
info: |
  ## Chat API Migration Guide: V1 to V3
  Complete guide for migrating from single endpoint to REST architecture
class: text-center text-sm
drawings:
  persist: false
transition: slide-left
mdc: true
headings: 
  level: small
---

<style>
h1 { @apply text-2xl !important; }
h2 { @apply text-lg !important; }
h3 { @apply text-base !important; }
h4 { @apply text-sm !important; }
.slidev-layout h1 { @apply text-2xl !important; }
.slidev-layout h2 { @apply text-lg !important; }
.slidev-layout h3 { @apply text-base !important; }
</style>

# Chat API Migration Guide

From V1 (/v2/complete) to V3 (/api/...)

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover:bg="white hover:bg-opacity-10">
    Single Endpoint → REST Architecture <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub" title="Open in GitHub" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:logo-github />
  </a>
</div>