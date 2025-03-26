

```vue file="src/layouts/DefaultLayout.vue" type="code" project="src/layouts/DefaultLayout"
[v0-no-op-code-block-prefix]<template>
  <div class="layout-page">
    <!-- Kozmik Başlık Bileşeni -->
    <div v-if="showCosmicTitle" class="mb-6">
      <CosmicTitle />
      <div class="flex justify-end">
        <button 
          @click="showCosmicTitle = false" 
          class="text-xs text-slate-400 hover:text-cyan-400 transition-colors"
        >
          <Icon icon="mdi:close" class="mr-1" />
          Başlığı Gizle
        </button>
      </div>
    </div>
    <button 
      v-else 
      @click="showCosmicTitle = true" 
      class="mb-4 text-sm text-slate-400 hover:text-cyan-400 transition-colors flex items-center"
    >
      <Icon icon="mdi:chevron-down" class="mr-1" />
      Kozmik Başlığı Göster
    </button>

    <!-- 👉 Pages -->
    <div style="min-height: calc(100vh - 180px)">
      <RouterView v-slot="{ Component }">
        <Transition mode="out-in">
          <Component :is="Component" />
        </Transition>
      </RouterView>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { RouterView } from 'vue-router'
import CosmicTitle from '@/components/CosmicTitle.vue'
import Icon from '@/components/Icon.vue'

const showCosmicTitle = ref(true)
</script>
