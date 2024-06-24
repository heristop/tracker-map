<script setup lang="ts">
import { computed } from 'vue'
import domtoimage from 'dom-to-image'
import TButton from './ui/TButton.vue'
import { useStore } from '~/composables/store'

const store = useStore()

const minWidth = computed({
  get: () => store.minWidth,
  set: value => store.minWidth = value,
})

const minHeight = computed({
  get: () => store.minHeight,
  set: value => store.minHeight = value,
})

const captureTreeMap = () => {
  const projectMapElement = document.querySelector('.tree-map') as HTMLElement | null

  if (projectMapElement) {
    window.scrollTo(0, 0)
    nextTick(() => {
      domtoimage.toPng(projectMapElement, { quality: 1, bgcolor: 'white' })
        .then((dataUrl: string) => {
          const link = document.createElement('a')
          link.href = dataUrl
          link.download = `tree-map-${Date.now()}.png`
          link.click()
        })
        .catch((error: Error) => {
          console.error('Error: ', error)
        })
    })
  }
  else {
    console.error('TreeMap section is not found')
  }
}
</script>

<template>
  <div class="flex items-center justify-between mb-3">
    <TButton
      :is-active="false"
      :disabled="!store.configLoaded"
      @click="captureTreeMap"
    >
      <svg
        class="w-5 h-5 text-white"
        aria-hidden="true"
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
      >
        <path
          stroke="currentColor"
          stroke-linejoin="round"
          stroke-width="2"
          d="M4 18V8a1 1 0 0 1 1-1h1.5l1.707-1.707A1 1 0 0 1 8.914 5h6.172a1 1 0 0 1 .707.293L17.5 7H19a1 1 0 0 1 1 1v10a1 1 0 0 1-1 1H5a1 1 0 0 1-1-1Z"
        />
        <path
          stroke="currentColor"
          stroke-linejoin="round"
          stroke-width="2"
          d="M15 12a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z"
        />
      </svg>
      <span class="text-sm">capture</span>
    </TButton>
  </div>

  <div class="flex items-center space-x-4 mb-4 px-2">
    <div class="flex flex-col items-start space-y-2">
      <span class="text-xs font-bold">Width</span>
      <input
        v-model="minWidth"
        type="range"
        min="0"
        max="500"
        class="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer"
      >
    </div>
    <div class="flex flex-col items-start space-y-2">
      <span class="text-xs font-bold">Height</span>
      <input
        v-model="minHeight"
        type="range"
        min="0"
        max="500"
        class="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer"
      >
    </div>
  </div>
</template>