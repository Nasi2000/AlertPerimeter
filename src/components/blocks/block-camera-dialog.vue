<template>
  <div v-if="modelValue" class="dialog-backdrop">
    <div class="dialog">
      <h2>Добавить камеру</h2>
      <label for="url">Ссылка на поток (RTSP/HTTP) или че тут хз :</label>
      <input id="url" v-model="url" type="text" placeholder="Введите ссылку" />

      <div class="dialog__actions">
        <button @click="submit">Подключить</button>
        <button class="cancel" @click="emit('update:modelValue', false)">Отмена</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { defineProps, defineEmits, ref } from 'vue'

const props = defineProps<{ modelValue: boolean }>()
const emit = defineEmits(['update:modelValue', 'submit'])

const url = ref('')

const submit = () => {
  if (!url.value) return
  emit('submit', url.value)
  emit('update:modelValue', false)
  url.value = ''
}
</script>

<style scoped>
.dialog-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.dialog {
  background: #1e1e1e;
  padding: 2rem;
  border-radius: 8px;
  width: 100%;
  max-width: 400px;
  color: white;
}

.dialog input {
  width: 100%;
  margin-top: 0.5rem;
  padding: 0.5rem;
  border-radius: 4px;
  border: none;
  background: #2e2e2e;
  color: white;
}

.dialog__actions {
  display: flex;
  justify-content: flex-end;
  margin-top: 1rem;
  gap: 0.5rem;
}

.dialog__actions button {
  padding: 0.5rem 1rem;
  background-color: #2196f3;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.dialog__actions .cancel {
  background-color: #757575;
}
</style>