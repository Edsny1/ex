<script lang="ts" setup>
import { Icon } from '@iconify/vue';
import { onMounted, ref } from 'vue';
import { useRouter } from 'vue-router';

import { useBlockchain } from '@/stores';
const vueRouters = useRouter();
const blockStore = useBlockchain();
let searchModalShow = ref(false);
let searchQuery = ref('');
let errorMessage = ref('');
onMounted(() => {});

function closeSearchModal() {
  searchModalShow.value = false;
}
function openSearchModal() {
  searchModalShow.value = true;
  // Modal açıldığında input'a odaklan
  setTimeout(() => {
    const inputElement = document.querySelector('.search-input') as HTMLInputElement;
    if (inputElement) inputElement.focus();
  }, 100);
}

function preventClick(event: any) {
  event.preventDefault();
  event.stopPropagation();
}
function confirm() {
  errorMessage.value = '';
  const key = searchQuery.value;
  if (!key) {
    errorMessage.value = 'Please enter a value!';
    return;
  }
  const height = /^\d+$/;
  const txhash = /^[A-Z\d]{64}$/;
  const addr = /^[a-z\d]+1[a-z\d]{38,58}$/;

  const current = blockStore?.current?.chainName || '';
  const routeParams = vueRouters?.currentRoute?.value;

  if (!Object.values(routeParams?.params).includes(key)) {
    if (height.test(key)) {
      vueRouters.push({ path: `/${current}/block/${key}` });
      setTimeout(() => {
        closeSearchModal();
      }, 1000);
    } else if (txhash.test(key)) {
      vueRouters.push({ path: `/${current}/tx/${key}` });
      setTimeout(() => {
        closeSearchModal();
      }, 1000);
    } else if (addr.test(key)) {
      vueRouters.push({ path: `/${current}/account/${key}` });
      setTimeout(() => {
        closeSearchModal();
      }, 1000);
    } else {
      errorMessage.value = 'The input not recognized';
    }
  }
}

// ESC tuşu ile modalı kapatma
function handleKeyDown(event: KeyboardEvent) {
  if (event.key === 'Escape' && searchModalShow.value) {
    closeSearchModal();
  }
}

onMounted(() => {
  window.addEventListener('keydown', handleKeyDown);
});
</script>

<template>
  <div>
    <button
      class="text-slate-300 hover:text-cyan-400 transition-colors"
      @click="openSearchModal"
    >
      <Icon
        icon="mdi:magnify"
        class="text-xl"
      />
    </button>

    <!-- modal -->
    <div
      v-if="searchModalShow"
      class="fixed inset-0 flex items-center justify-center z-[100] cosmic-search-modal"
      @click="closeSearchModal"
    >
      <div class="absolute inset-0 bg-black/70 backdrop-blur-sm"></div>
      
      <div
        class="relative w-full max-w-md mx-auto bg-[#0a1a3a] border border-[#4facfe]/30 rounded-xl shadow-lg p-5 transform transition-all z-[101]"
        @click="(event) => preventClick(event)"
      >
        <!-- header -->
        <div class="flex items-center justify-between mb-4">
          <div
            class="text-lg font-bold flex flex-col md:!flex-row justify-between items-baseline"
          >
            <span class="mr-2 text-cyan-400">Search</span>
            <span class="capitalize text-sm md:!text-base text-slate-300"
              >Height/Transaction/Account Address</span
            >
          </div>
          <button
            class="text-slate-400 hover:text-cyan-400 transition-colors"
            @click="closeSearchModal"
          >
            <Icon
              icon="mdi:close"
              class="text-xl"
            />
          </button>
        </div>
        
        <!-- body -->
        <div class="mt-4">
          <div class="relative">
            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
              <Icon icon="mdi:magnify" class="text-xl text-slate-400" />
            </div>
            <input
              class="w-full pl-10 pr-4 py-3 bg-[#0a1a3a] border border-[#4facfe]/30 rounded-xl focus:outline-none focus:ring-2 focus:ring-[#4facfe]/50 text-slate-200 search-input"
              v-model="searchQuery"
              placeholder="Height/Transaction/Account Address"
            />
            <div
              class="mt-2 text-right text-sm text-red-500"
              v-show="errorMessage"
            >
              {{ errorMessage }}
            </div>
          </div>
        </div>
        
        <!-- foot -->
        <div class="mt-6">
          <button 
            class="w-full py-3 bg-gradient-to-r from-[#4facfe] to-[#00f2fe] hover:opacity-90 text-white font-medium rounded-xl transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-[#4facfe]/50" 
            @click="confirm"
          >
            Confirm
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.cosmic-search-modal {
  animation: fadeIn 0.2s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

/* Responsive düzenlemeler */
@media (max-width: 640px) {
  .cosmic-search-modal > div:last-child {
    margin: 0 1rem;
    max-width: none;
  }
}
</style>
