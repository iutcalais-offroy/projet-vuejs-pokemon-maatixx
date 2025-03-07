<template>
  <n-form @submit.prevent="handleSignIn">
    <n-form-item label="Email">
      <n-input v-model="email" type="email" placeholder="Entrez votre email" required />
    </n-form-item>
    <n-form-item label="Mot de passe">
      <n-input v-model="password" type="password" placeholder="Entrez votre mot de passe" required />
    </n-form-item>
    <n-form-item>
      <n-button type="primary" native-type="submit" block>Se connecter</n-button>
    </n-form-item>
  </n-form>
  <p>Pas de compte ? <a @click="$emit('switch-tab', 'register')">S'inscrire</a></p>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router';

const email = ref('');
const password = ref('');
const router = useRouter();

const handleSignIn = async () => {
  try {
    const response = await axios.post(`${import.meta.env.VITE_API_URL}/users/login`, {
      email: email.value,
      password: password.value
    });
    localStorage.setItem('token', response.data.token);
    localStorage.setItem('userId', response.data.userId);
    router.push('/deck-builder');
  } catch (error) {
    console.error('Erreur de connexion', error);
  }
};
</script>

<style scoped>
p {
  text-align: center;
  margin-top: 10px;
}

p a {
  color: #18a058;
  cursor: pointer;
  text-decoration: none;
}
</style>