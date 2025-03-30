<template>
  <header class="menu">
    <div class="menu__logo">AlertVision AI</div>
    <nav class="menu__nav">
      <button @click="goTo('/')">Главная</button>
      <button @click="goTo('/cameras')">Камеры</button>
      <button @click="goTo('/subscription')">Подписка</button>
      <button @click="goTo('/settings')">Настройки</button>
    </nav>
    <button class="menu__logout" @click="logout">Выход</button>
  </header>
</template>

<script lang="ts" setup>
import { useRouter } from 'vue-router'
const router = useRouter()

const goTo = (path: string) => {
  router.push(path)
}

const logout = () => {
  router.push('/login')
}
</script>

<style scoped>
.menu {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: #1e1e1e;
  color: #fff;
}

.menu__logo {
  font-size: 1.25rem;
  font-weight: bold;
}

.menu__nav button {
  margin: 0 0.5rem;
  background: none;
  border: none;
  color: inherit;
  font-size: 1rem;
  cursor: pointer;
}

.menu__nav button:hover,
.menu__logout:hover {
  color: #00bcd4;
}

.menu__logout {
  background: none;
  border: none;
  color: inherit;
  font-size: 1rem;
  cursor: pointer;
}
</style>