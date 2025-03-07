<template>
  <n-card>
    <n-tabs v-model:value="activeTab" type="line" animated>
      <n-tab-pane name="login" tab="Connexion">
        <SignIn @switch-tab="switchTab" />
      </n-tab-pane>
      
      <n-tab-pane name="register" tab="Inscription">
        <Register @switch-tab="switchTab" />
      </n-tab-pane>
    </n-tabs>
  </n-card>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import SignIn from '../components/SignIn.component.vue';
import Register from '../components/Register.component.vue';

const activeTab = ref<'login' | 'register'>('login');
const switchTab = (tab: 'login' | 'register') => {
  activeTab.value = tab;
};
</script>

<style scoped>
p {
  text-align: center;
  margin-top: 10px;
}
</style>