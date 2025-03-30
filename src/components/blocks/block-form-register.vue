<template>
  <div class="container">
    <form class="register-form" @submit.prevent="handleSubmit">
      <div class="ring">
        <i></i>
        <i></i>
        <i></i>

        <div class="login-form">
          <h2>Register</h2>
          <div class="inputBx">
            <input
              v-model="form.username"
              type="text"
              placeholder="Username"
            />
            <span v-if="errors.username">{{ errors.username }}</span>
          </div>

          <div class="inputBx">
            <input
              v-model="form.email"
              type="email"
              placeholder="Email"
            />
            <span v-if="errors.email">{{ errors.email }}</span>
          </div>

          <div class="inputBx">
            <input
              v-model="form.password"
              type="password"
              placeholder="Password"
            />
            <span v-if="errors.password">{{ errors.password }}</span>
          </div>

          <div class="actions">
            <Button type="submit" class="submit">Зарегистрироваться</Button>
            <RouterLink to="/auth" class="link">Войти</RouterLink>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script lang="ts" setup>
import { reactive } from 'vue'
import axios from 'axios'
import { toast } from 'vue3-toastify'
import router from '@/router'

interface RegisterForm {
  username: string
  email: string
  password: string
}

const form = reactive<RegisterForm>({
  username: '',
  email: '',
  password: '',
})

const errors = reactive<Partial<RegisterForm>>({})

const validate = (): boolean =>{
  errors.username = form.username ? '' : 'Введите имя'
  errors.email = /\S+@\S+\.\S+/.test(form.email) ? '' : 'Введите email'
  errors.password = form.password.length >= 6 ? '' : 'Пароль должен содержать не менее 6 символов'

  return !errors.username && !errors.email && !errors.password
}

const handleSubmit = async () => {
  if (!validate()) return

  try {
    const response = await axios.post('http://37.195.129.183:8000/register', {
      username: form.username,
      email: form.email,
      password: form.password,
    })
    toast.success('Успешно')
    router.push('/home')
  } catch (error) {
    console.error('Ошибка входа:', error)
    toast.error('Ошибка входа')
  }
}
</script>

<style scoped>

.ring {
  position: relative;
  width: 400px;
  height: 400px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.ring i {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: 4px solid #ffffff30;
  box-sizing: border-box;
  border-radius: 38% 62% 63% 37% / 41% 44% 56% 59%;
  animation: animate 6s linear infinite;
  transition: 0.5s;
}

.ring i:nth-child(2) {
  transform: scale(1.1);
  animation-duration: 4s;
  border-radius: 41% 44% 56% 59% / 38% 62% 63% 37%;
}

.ring i:nth-child(3) {
  transform: scale(1.2);
  animation-duration: 10s;
  border-radius: 41% 44% 56% 59% / 38% 62% 63% 37%;
}

.ring:hover i:nth-child(1) {
  border: 6px solid lawngreen;
  filter: drop-shadow(0 0 20px lawngreen);
}

.ring:hover i:nth-child(2) {
  border: 6px solid red;
  filter: drop-shadow(0 0 20px red);
}

.ring:hover i:nth-child(3) {
  border: 6px solid yellow;
  filter: drop-shadow(0 0 20px yellow);
}

@keyframes animate {
  0% {
    transform: rotate(0deg) scale(1);
  }
  100% {
    transform: rotate(360deg) scale(1);
  }
}

.login-form {
  position: relative;
  z-index: 1;
  padding: 2rem;
  border-radius: 16px;
  width: 100%;
  max-width: 300px;
}

.container {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  overflow: hidden;
}

.register-form {
  color: #fff;
}

h2 {
  text-align: center;
  margin-bottom: 1rem;
}

.inputBx {
  margin-bottom: 1rem;
}

input[type="text"],
input[type="email"],
input[type="password"] {
  width: 100%;
  padding: 0.75rem;
  background: #181818;
  border: 0.5px solid #fff;
  border-radius: 50px;
  color: #fff;
}

span {
  color: #ff4d4d;
  font-size: 0.8rem;
}

.actions{
  display: flex;
  flex-direction: column;
  gap: 20px
}


.submit {
  width: 100%;
  padding: 15px 50px;
  background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(121,51,9,1) 0%, rgba(171,92,5,1) 41%, rgba(243,255,0,1) 100%);
  color: white;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  font-weight: bold;

  &:hover {
    background: #45a049;
  }
}

.link{
  color: #fff;
  font-size: 10px;
  text-decoration: none;

  &:hover{
    color: yellow;
  }
}
</style>