<template>
  <div
    class="fixed top-0 z-40 h-16 w-full border-b bg-white p-2 lg:h-20"
    data-testid="layoutHeader"
  >
    <div class="container mx-auto flex items-center">
      <NuxtLink to="/" @click="mobileNavigationVisible = false"
        ><AppLayoutLogo
      /></NuxtLink>

      <div class="relative ml-auto flex">
        <AppLayoutNavigation class="hidden md:flex" />
        <transition name="fadeup">
          <AppLayoutMobileNavigation
            v-if="mobileNavigationVisible"
            class="-z-10 md:hidden"
            @close="mobileNavigationVisible = false"
          />
        </transition>

        <AppLayoutLanguageSwitch
          class="ml-2"
          @language-switch="mobileNavigationVisible = false"
        />
        <button
          class="md:hidden"
          data-testid="mobileMenuButton"
          @click="mobileNavigationVisible = !mobileNavigationVisible"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="h-6 w-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"
            />
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const mobileNavigationVisible = ref(false)
</script>
