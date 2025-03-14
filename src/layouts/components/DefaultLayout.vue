<script lang="ts" setup>
import { Icon } from '@iconify/vue';
import { ref } from 'vue';

// Components
import newFooter from '@/layouts/components/NavFooter.vue';
import NavbarThemeSwitcher from '@/layouts/components/NavbarThemeSwitcher.vue';
import NavbarSearch from '@/layouts/components/NavbarSearch.vue';
import ChainProfile from '@/layouts/components/ChainProfile.vue';

import { useDashboard } from '@/stores/useDashboard';
import { useBlockchain } from '@/stores';

import NavBarI18n from './NavBarI18n.vue';
import NavBarWallet from './NavBarWallet.vue';
import type {
  NavGroup,
  NavLink,
  NavSectionTitle,
  VerticalNavItems,
} from '../types';

const dashboard = useDashboard();
dashboard.initial();
const blockchain = useBlockchain();
blockchain.randomSetupEndpoint();

const current = ref(''); // the current chain
const temp = ref('');
blockchain.$subscribe((m, s) => {
  if (current.value === s.chainName && temp.value != s.endpoint.address) {
    temp.value = s.endpoint.address;
    blockchain.initial();
  }
  if (current.value != s.chainName) {
    current.value = s.chainName;
    blockchain.randomSetupEndpoint();
  }
});

const sidebarShow = ref(false);
const sidebarOpen = ref(true);

const changeOpen = (index: Number) => {
  if (index === 0) {
    sidebarOpen.value = !sidebarOpen.value;
  }
};
const showDiscord = window.location.host.search('ping.pub') > -1;

function isNavGroup(nav: VerticalNavItems | any): nav is NavGroup {
  return (<NavGroup>nav).children !== undefined;
}
function isNavLink(nav: VerticalNavItems | any): nav is NavLink {
  return (<NavLink>nav).to !== undefined;
}
function isNavTitle(nav: VerticalNavItems | any): nav is NavSectionTitle {
  return (<NavSectionTitle>nav).heading !== undefined;
}
function selected(route: any, nav: NavLink) {
  const b =
    route.path === nav.to?.path ||
    (route.path.startsWith(nav.to?.path) &&
      nav.title.indexOf('dashboard') === -1);
  return b;
}
</script>

<template>
  <div class="bg-gray-100 dark:bg-[#171d30]">
    <!-- sidebar -->
    <div
      class="w-64 fixed z-50 left-0 top-0 bottom-0 overflow-auto oshvank-sidebar"
      :class="{ block: sidebarShow, 'hidden xl:!block': !sidebarShow }"
    >
      <div class="flex justify-between mt-1 pl-4 py-4 mb-1 sidebar-header">
        <RouterLink to="/" class="flex items-center">
          <img src="/favicon.ico" alt="Logo" class="w-8 h-8" />
          <h1 class="flex-1 ml-3 text-2xl font-semibold oshvank-logo-text">
            OshVanK
          </h1>
        </RouterLink>
        <div
          class="pr-4 cursor-pointer xl:!hidden"
          @click="sidebarShow = false"
        >
          <Icon icon="mdi-close" class="text-2xl text-slate-300 hover:text-white transition-colors" />
        </div>
      </div>
      <div
        v-for="(item, index) of blockchain.computedChainMenu"
        :key="index"
        class="px-2"
      >
        <div
          v-if="isNavGroup(item)"
          :tabindex="index"
          class="collapse"
          :class="{
            'collapse-arrow': item?.children?.length > 0,
            'collapse-open': index === 0 && sidebarOpen,
            'collapse-close': index === 0 && !sidebarOpen,
          }"
        >
          <input
            type="checkbox"
            class="cursor-pointer !h-10 block"
            @click="changeOpen(index)"
          />
          <div
            class="collapse-title !py-0 px-4 flex items-center cursor-pointer oshvank-menu-group"
          >
            <Icon
              v-if="item?.icon?.icon"
              :icon="item?.icon?.icon"
              class="text-xl mr-2"
              :class="{
                'text-yellow-400': item?.title === 'Favorite',
                'text-cyan-400': item?.title !== 'Favorite',
              }"
            />
            <img
              v-if="item?.icon?.image"
              :src="item?.icon?.image"
              class="w-6 h-6 rounded-full mr-3"
            />
            <div
              class="text-base capitalize flex-1 text-slate-200 whitespace-nowrap"
            >
              {{ item?.title }}
            </div>
            <div
              v-if="item?.badgeContent"
              class="menu-badge"
              :class="item?.badgeClass"
            >
              {{ item?.badgeContent }}
            </div>
          </div>
          <div class="collapse-content">
            <div
              v-for="(el, key) of item?.children"
              class="menu w-full !p-0"
            >
              <RouterLink
                v-if="isNavLink(el)"
                @click="sidebarShow = false"
                class="oshvank-menu-item"
                :class="{
                  'oshvank-menu-item-active': selected($route, el),
                }"
                :to="el.to"
              >
                <Icon
                  v-if="!el?.icon?.image"
                  icon="mdi:chevron-right"
                  class="mr-2 ml-3 text-slate-500"
                  :class="{
                    'text-cyan-400': selected($route, el),
                  }"
                />
                <img
                  v-if="el?.icon?.image"
                  :src="el?.icon?.image"
                  class="w-6 h-6 rounded-full mr-3 ml-4"
                  :class="{
                    'border border-gray-300 bg-white': selected($route, el),
                  }"
                />
                <div
                  class="text-sm capitalize text-slate-300"
                  :class="{
                    'text-cyan-400': selected($route, el),
                  }"
                >
                  {{ item?.title === 'Favorite' ? el?.title : $t(el?.title) }}
                </div>
              </RouterLink>
            </div>
          </div>
        </div>

        <RouterLink
          v-if="isNavLink(item) && item?.title === 'Favorite'"
          :to="item?.to"
          @click="sidebarShow = false"
          class="oshvank-menu-item menu-item-favorite"
        >
          <Icon
            v-if="item?.icon?.icon"
            :icon="item?.icon?.icon"
            class="text-xl mr-2 text-yellow-400"
          />
          <img
            v-if="item?.icon?.image"
            :src="item?.icon?.image"
            class="w-6 h-6 rounded-full mr-3"
          />
          <div class="text-sm capitalize flex-1 text-yellow-400 whitespace-nowrap">
            {{ item?.title }}
          </div>
        </RouterLink>

        <RouterLink
          v-else-if="isNavLink(item) && item?.title === 'All Blockchains'"
          :to="item?.to"
          @click="sidebarShow = false"
          class="oshvank-menu-item menu-item-all-chains"
        >
          <Icon
            v-if="item?.icon?.icon"
            :icon="item?.icon?.icon"
            class="text-xl mr-2 text-cyan-400"
          />
          <img
            v-if="item?.icon?.image"
            :src="item?.icon?.image"
            class="w-6 h-6 rounded-full mr-3"
          />
          <div class="text-sm capitalize flex-1 text-slate-200 whitespace-nowrap">
            {{ item?.title }}
          </div>
          <div
            v-if="item?.badgeContent"
            class="menu-badge"
          >
            {{ item?.badgeContent }}
          </div>
        </RouterLink>

        <RouterLink
          v-else-if="isNavLink(item)"
          :to="item?.to"
          @click="sidebarShow = false"
          class="oshvank-menu-item"
        >
          <Icon
            v-if="item?.icon?.icon"
            :icon="item?.icon?.icon"
            class="text-xl mr-2 text-cyan-400"
          />
          <img
            v-if="item?.icon?.image"
            :src="item?.icon?.image"
            class="w-6 h-6 rounded-full mr-3"
          />
          <div class="text-sm capitalize flex-1 text-slate-300 whitespace-nowrap">
            {{ item?.title }}
          </div>
          <div
            v-if="item?.badgeContent"
            class="menu-badge"
          >
            {{ item?.badgeContent }}
          </div>
        </RouterLink>

        <div
          v-if="isNavTitle(item)"
          class="oshvank-menu-section"
        >
          {{ item?.heading }}
        </div>
      </div>
      <div class="px-2">
        <div class="oshvank-menu-section">
          {{ $t('module.sponsors') }}
        </div>
        <a
          href="https://osmosis.zone"
          target="_blank"
          class="oshvank-menu-item"
        >
          <img
            src="https://ping.pub/logos/osmosis.jpg"
            class="w-6 h-6 rounded-full mr-3"
          />
          <div class="text-sm capitalize flex-1 text-slate-300">
            Osmosis
          </div>
        </a>
        <a
          href="https://celestia.org"
          target="_blank"
          class="oshvank-menu-item"
        >
          <img
            src="https://ping.pub/logos/celestia.png"
            class="w-6 h-6 rounded-full mr-3"
          />
          <div class="text-sm capitalize flex-1 text-slate-300">
            Celestia
          </div>
        </a>
        <a
          href="https://becole.com"
          target="_blank"
          class="oshvank-menu-item"
        >
          <img
            src="https://becole.com/static/logo/logo_becole.png"
            class="w-6 h-6 rounded-full mr-3"
          />
          <div class="text-sm capitalize flex-1 text-slate-300">
            Becole
          </div>
        </a>

        <div class="oshvank-menu-section">Tools</div>
        <RouterLink
          to="/wallet/suggest"
          class="oshvank-menu-item"
        >
          <Icon icon="mdi:frequently-asked-questions" class="text-xl mr-2 text-cyan-400" />
          <div class="text-sm capitalize flex-1 text-slate-300">
            Wallet Helper
          </div>
        </RouterLink>

        <div class="oshvank-menu-section">
          {{ $t('module.links') }}
        </div>
        <a
          href="https://twitter.com/"
          target="_blank"
          class="oshvank-menu-item"
        >
          <Icon icon="mdi:twitter" class="text-xl mr-2 text-cyan-400" />
          <div class="text-sm capitalize flex-1 text-slate-300">
            Twitter
          </div>
        </a>
        <a
          v-if="showDiscord"
          href="https://discord.com/users/132567842431172608"
          target="_blank"
          class="oshvank-menu-item"
        >
          <Icon icon="mdi:discord" class="text-xl mr-2 text-cyan-400" />
          <div class="text-sm capitalize flex-1 text-slate-300">
            Discord
          </div>
        </a>
        <a
          href="https://github.com/ping-pub/explorer/discussions"
          target="_blank"
          class="oshvank-menu-item"
        >
          <Icon icon="mdi:frequently-asked-questions" class="text-xl mr-2 text-cyan-400" />
          <div class="text-sm capitalize flex-1 text-slate-300">
            FAQ
          </div>
        </a>
      </div>
    </div>
    <div class="xl:!ml-64 px-3 pt-4">
      <!-- header -->
      <div
        class="flex items-center py-3 mb-4 rounded px-4 sticky top-0 z-10 oshvank-header"
      >
        <div
          class="text-2xl pr-3 cursor-pointer xl:!hidden text-slate-300 hover:text-cyan-400 transition-colors"
          @click="sidebarShow = true"
        >
          <Icon icon="mdi-menu" />
        </div>

        <ChainProfile />

        <div class="flex-1 w-0"></div>

        <!-- <NavSearchBar />-->
        <NavBarI18n class="hidden md:!inline-block" />
        <NavbarThemeSwitcher class="!inline-block" />
        <NavbarSearch class="!inline-block" />
        <NavBarWallet />
      </div>

      <!-- 👉 Pages -->
      <div style="min-height: calc(100vh - 180px)">
        <RouterView v-slot="{ Component }">
          <Transition mode="out-in">
            <Component :is="Component" />
          </Transition>
        </RouterView>
      </div>

      <newFooter />
    </div>
  </div>
</template>

<style scoped>
/* Sidebar Stilleri */
.oshvank-sidebar {
  background-color: #171d30;
  border-right: 1px solid rgba(100, 116, 139, 0.2);
}

.sidebar-header {
  border-bottom: 1px solid rgba(100, 116, 139, 0.2);
  padding: 0.5rem 0;
}

.oshvank-logo-text {
  background: linear-gradient(to right, #22d3ee, #0ea5e9);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.oshvank-menu-group {
  margin: 2px 0;
  border-radius: 0.375rem;
  transition: all 0.2s ease;
  padding: 0.5rem 0.75rem;
}

.oshvank-menu-group:hover {
  background-color: rgba(30, 41, 59, 0.5);
}

.oshvank-menu-item {
  display: flex;
  align-items: center;
  padding: 0.625rem 0.75rem;
  margin: 2px 0;
  border-radius: 0.375rem;
  cursor: pointer;
  transition: all 0.2s ease;
  color: #94a3b8;
  font-size: 0.875rem;
  background-color: transparent;
}

.oshvank-menu-item:hover {
  background-color: rgba(30, 41, 59, 0.5);
  color: #e2e8f0;
}

.oshvank-menu-item-active {
  background-color: rgba(30, 41, 59, 0.8) !important;
  color: #0ea5e9 !important;
}

.oshvank-menu-section {
  padding: 1.25rem 0.75rem 0.5rem 0.75rem;
  font-size: 0.75rem;
  font-weight: 500;
  text-transform: uppercase;
  color: #64748b;
  letter-spacing: 0.05em;
}

/* Özel menü öğeleri için stiller */
.menu-item-favorite {
  color: #fbbf24 !important;
}

.menu-item-all-chains {
  position: relative;
  color: #e2e8f0 !important;
}

.menu-badge {
  background-color: #ef4444;
  color: white;
  font-size: 0.75rem;
  padding: 0.125rem 0.375rem;
  border-radius: 9999px;
  margin-left: auto;
}

/* Header Stilleri */
.oshvank-header {
  background-color: #171d30;
  border: 1px solid rgba(100, 116, 139, 0.2);
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0
