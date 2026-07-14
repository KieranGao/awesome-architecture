<script setup lang="ts">
import { useData } from 'vitepress'
import { computed, ref } from 'vue'

defineProps<{
  title: string
  a: string
  aDesc: string
  b: string
  bDesc: string
  verdict: string
}>()

const show = ref(false)
const { lang } = useData()

const isEn = computed(() => lang.value?.startsWith('en'))
const toggleLabel = computed(() => {
  if (show.value) return isEn.value ? 'Collapse ▲' : '收起 ▲'
  return isEn.value ? '👉 What would an architect usually choose? ▼' : '👉 架构师通常怎么选?▼'
})
</script>

<template>
  <div class="dc">
    <div class="dc-title"><span>⚖️</span>{{ title }}</div>
    <div class="dc-cols">
      <div class="dc-col">
        <div class="dc-h">{{ a }}</div>
        <div class="dc-d">{{ aDesc }}</div>
      </div>
      <div class="dc-vs">VS</div>
      <div class="dc-col">
        <div class="dc-h">{{ b }}</div>
        <div class="dc-d">{{ bDesc }}</div>
      </div>
    </div>
    <button type="button" class="dc-btn" :aria-expanded="show" @click="show = !show">
      {{ toggleLabel }}
    </button>
    <div v-if="show" class="dc-verdict">{{ verdict }}</div>
  </div>
</template>

<style scoped>
.dc {
  border: 1px solid var(--vp-c-divider); border-radius: 12px;
  padding: 18px 20px; margin: 24px 0; background: var(--vp-c-bg-soft);
}
.dc-title { font-weight: 600; margin-bottom: 14px; }
.dc-title span { margin-right: 8px; }
.dc-cols { display: flex; align-items: stretch; gap: 12px; }
.dc-col { flex: 1; padding: 14px; border: 1px solid var(--vp-c-divider); border-radius: 8px; background: var(--vp-c-bg); }
.dc-h { font-weight: 600; margin-bottom: 6px; color: var(--vp-c-text-1); }
.dc-d { font-size: 13px; color: var(--vp-c-text-2); line-height: 1.55; }
.dc-vs { display: flex; align-items: center; font-size: 12px; font-weight: 700; color: var(--vp-c-text-3); }
.dc-btn {
  margin-top: 14px; font-size: 14px; padding: 7px 16px;
  border: 1px solid var(--vp-c-brand-1); border-radius: 8px;
  background: var(--vp-c-brand-soft); color: var(--vp-c-brand-1); cursor: pointer; transition: 0.2s;
}
.dc-btn:hover { background: var(--vp-c-brand-1); color: #fff; }
.dc-verdict {
  margin-top: 12px; padding: 12px 14px; border-radius: 8px;
  background: var(--vp-c-brand-soft); font-size: 14px; line-height: 1.65; color: var(--vp-c-text-1);
}
@media (max-width: 640px) {
  .dc-cols { flex-direction: column; }
  .dc-vs { justify-content: center; }
}
</style>
