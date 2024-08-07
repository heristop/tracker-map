<script setup lang="ts">
import { computed } from 'vue'
import { useStore } from '~/composables/store'
import type { Section } from '~~/types'

const store = useStore()
const statuses = computed(() => store.statuses)

const totalModules = computed(() => {
  const count = (modules: Section[]): number => {
    return modules.reduce((acc: number, module: Section) => {
      acc++

      if (module.children) {
        acc += count(module.children)
      }

      return acc
    }, 0)
  }
  return count(store.sections)
})

const countComponentsByStatus = (status: string) => {
  const count = (modules: Section[]) => {
    return modules.reduce((acc, module) => {
      if (module.status === status) {
        acc++
      }

      if (module.children) {
        acc += count(module.children)
      }

      return acc
    }, 0)
  }
  return count(store.sections)
}

const statusPercentage = (status: string) => {
  const count = countComponentsByStatus(status)
  return totalModules.value ? (count / totalModules.value) * 100 : 0
}
</script>

<template>
  <div class="flex w-full shadow-md h-4 bg-gray-300 rounded-lg overflow-hidden mb-4">
    <div
      v-for="status in statuses"
      :key="status.name"
      class="h-full transition-width duration-300 ease-in-out"
      :style="{ width: statusPercentage(status.name) + '%', backgroundColor: status.color }"
    />
  </div>
</template>
