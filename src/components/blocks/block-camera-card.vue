<template>
  <div class="camera-card" :class="camera.status">
    <img :src="camera.image" alt="Camera preview" class="camera-card__image" />
    <div class="camera-card__info">
      <div class="camera-card__status">
        Статус: <span :class="camera.status">{{ camera.status }}</span>
      </div>
      <div>Объектов обнаружено: <strong>{{ camera.objects }}</strong></div>
      <div class="camera-card__actions">
        <button @click="viewCamera">Просмотр</button>
        <button @click="editCamera">Настроить</button>
        <button @click="deleteCamera">Удалить</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { defineProps, defineEmits } from 'vue'


const props = defineProps<{
  camera: {
    id: number
    image: string
    status: 'online' | 'offline'
    objects: number
  }
}>()

const emit = defineEmits(['view', 'edit', 'delete'])

const viewCamera = () => emit('view', props.camera.id)
const editCamera = () => emit('edit', props.camera.id)
const deleteCamera = () => emit('delete', props.camera.id)

</script>

<style scoped>
.camera-card {
  display: flex;
  flex-direction: column;
  background: #2c2c2c;
  border-radius: 8px;
  overflow: hidden;
  width: 100%;
  max-width: 320px;
  margin-right: 1rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.camera-card__image {
  width: 100%;
  height: 180px;
  object-fit: cover;
}

.camera-card__info {
  padding: 1rem;
  color: white;
}

.camera-card__status span.online {
  color: #4caf50;
}

.camera-card__status span.offline {
  color: #f44336;
}

.camera-card__actions {
  margin-top: 0.5rem;
  display: flex;
  justify-content: space-between;
  gap: 0.5rem;
}

.camera-card__actions button {
  flex: 1;
  background: #424242;
  color: white;
  border: none;
  padding: 0.5rem;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.875rem;
}

.camera-card__actions button:hover {
  background: #616161;
}
</style>