<template>
  <BlockMenu/>

  <div style="display: flex; flex-wrap: wrap; gap: 1rem; margin-top: 1rem;">
    <BlockCameraCard
      v-for="camera in cameras"
      :key="camera.id"
      :camera="camera"
      @view="handleView"
      @edit="handleEdit"
      @delete="handleDelete"
    />
  </div>

  <button @click="dialog = true" style="margin-top: 1rem;">Добавить камеру</button>

  <BlockCameraDialog v-model="dialog" @submit="handleAddCamera" />
</template>

<script setup lang="ts">
import { ref } from 'vue'
import BlockMenu from '@/components/shareds/menu.vue'
import BlockCameraCard from '@/components/blocks/block-camera-card.vue'
import BlockCameraDialog from '@/components/blocks/block-camera-dialog.vue'

const dialog = ref(false)

type Camera = {
  id: number
  image: string
  status: 'online' | 'offline'
  objects: number
}

const cameras = ref<Camera[]>([
  { id: 1, image: '/mock/placeholder.jpg', status: 'online', objects: 3 },
  { id: 2, image: '/mock/placeholder.jpg', status: 'offline', objects: 1 },
])

const handleView = (id: number) => {
  console.log('Просмотреть камеры', id)
}

const handleEdit = (id: number) => {
  console.log('Настройкаааа камеры', id)
}

const handleDelete = (id: number) => {
  cameras.value = cameras.value.filter(cam => cam.id !== id)
}

const handleAddCamera = (url: string) => {
  cameras.value.push({
    id: Date.now(),
    image: '/mock/placeholder.jpg',
    status: 'online',
    objects: 0,
  })
}
</script>

<style scoped>
</style>