<script lang="ts" setup>
import { useDashboard } from '@/stores/useDashboard';
import { computed } from 'vue';
import { Icon } from '@iconify/vue';

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
});

const dashboardStore = useDashboard();
const conf = computed(() => dashboardStore.chains[props.name] || {});

const addFavor = (e: Event) => {
  e.stopPropagation();
  e.preventDefault();
  dashboardStore.favoriteMap[props.name] =
    !dashboardStore?.favoriteMap?.[props.name];
  window.localStorage.setItem(
    'favoriteMap',
    JSON.stringify(dashboardStore.favoriteMap)
  );
};
</script>
<template>
  <RouterLink
    :to="`/${name}`"
    class="bg-base-100 hover:bg-gray-100 dark:hover:bg-[#373f59] rounded shadow flex items-center px-3 py-3 cursor-pointer oshvank-card"
  >
    <div class="w-8 h-8 rounded-full overflow-hidden oshvank-icon">
      <img :src="conf.logo" />
    </div>
    <div class="font-semibold ml-4 text-base flex-1 truncate capitalize">
      {{ conf?.prettyName || props.name }}
    </div>
    <div
      @click="addFavor"
      class="pl-4 text-xl oshvank-star"
      :class="{
        'text-warning active': dashboardStore?.favoriteMap?.[props.name],
        'text-gray-300 dark:text-gray-500':
          !dashboardStore?.favoriteMap?.[props.name],
      }"
    >
      <Icon icon="mdi-star" />
    </div>
  </RouterLink>
</template>

<style scoped>
.oshvank-card {
  background-color: var(--oshvank-card-bg) !important;
  backdrop-filter: blur(4px);
  border: 1px solid var(--oshvank-border) !important;
  border-radius: 0.75rem !important;
  padding: 1rem !important;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: space-between;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05) !important;
}

.oshvank-card:hover {
  border-color: var(--oshvank-hover-border) !important;
  box-shadow: 0 4px 12px var(--oshvank-shadow) !important;
  transform: translateY(-2px);
}

.oshvank-icon {
  background: linear-gradient(to bottom right, #334155, #1e293b);
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 2rem;
  min-height: 2rem;
}

.oshvank-star {
  transition: all 0.2s ease;
}

.oshvank-star:hover {
  color: var(--oshvank-primary) !important;
  transform: scale(1.2);
}

.oshvank-star.active {
  color: var(--oshvank-primary) !important;
}
</style>
