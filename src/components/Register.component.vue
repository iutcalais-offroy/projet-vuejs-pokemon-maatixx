<template>
  <n-form @submit.prevent="handleRegister">
    <n-form-item label="Nom">
      <n-input v-model="name" placeholder="Entrez votre nom" required />
    </n-form-item>
    <n-form-item label="Email">
      <n-input v-model="email" type="email" placeholder="Entrez votre email" required />
    </n-form-item>
    <n-form-item label="Mot de passe">
      <n-input v-model="password" type="password" placeholder="Entrez votre mot de passe" required />
    </n-form-item>
    <n-form-item label="Confirmer le mot de passe">
      <n-input v-model="confirmPassword" type="password" placeholder="Entrez votre mot de passe" required />
    </n-form-item>
    <n-form-item>
      <n-button type="primary" native-type="submit" block>S'inscrire</n-button>
    </n-form-item>
  </n-form>
  <p>Déjà inscrit ? <a @click="$emit('switch-tab', 'login')">Se connecter</a></p>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import axios from 'axios';

const name = ref('');
const email = ref('');
const password = ref('');
const confirmPassword = ref('');

const handleRegister = async () => {
  if (password.value !== confirmPassword.value) {
    console.error("Les mots de passe ne correspondent pas");
    return;
  }
  try {
    await axios.post(`${import.meta.env.VITE_API_URL}/users/`, {
      name: name.value,
      email: email.value,
      password: password.value
    });
  } catch (error) {
    console.error("Erreur d'inscription", error);
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