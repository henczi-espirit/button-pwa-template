<template>
  <div class="group relative h-64" data-testid="headerSection">
    <Dev
      v-if="showDev && $isPreviewMode"
      :content="data"
      class="hidden group-hover:block"
      component-name="Page Header"
    />
    <div
      class="absolute inset-0 flex flex-col justify-center bg-black bg-opacity-80 p-6 text-white md:p-12"
    >
      <div class="max-w-xl md:border-l-8 md:p-8">
        <h1 class="text-3xl font-black uppercase">{{ data['pt_title'] }}</h1>
        <!-- <p class="text-sm text-gray-300">{{ data.pt_text }}</p> -->
        <span
          v-for="(breadcrumb, index) in breadcrumbs"
          :key="'breadcrumb-' + index"
          class="mr-2 text-sm text-gray-300"
          >>
          <NuxtLink
            class="hover:underline"
            :to="'/' + breadcrumbs.slice(0, index + 1).join('/')"
            >{{ breadcrumb }}</NuxtLink
          ></span
        >
      </div>
    </div>
    <ElementsImage
      v-if="data['pt_picture']"
      class="h-full w-full object-cover"
      :image="data['pt_picture']"
    />
  </div>
</template>

<script setup lang="ts">
import { DataEntries } from 'fsxa-api'

defineProps<{ data: DataEntries }>()

const { $isPreviewMode } = useNuxtApp()

const { showDev } = useDev()

const breadcrumbs = computed(() => {
  const { slug } = useRoute().params
  return Array.isArray(slug) ? slug.filter((el) => el) : [slug]
})
</script>
