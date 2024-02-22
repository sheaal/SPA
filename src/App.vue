<template>
  <nav>
    <div>
      <router-link to="/">Home</router-link>
      <router-link to="/cart">Cart</router-link>
      <router-link to="/order">Order</router-link>
      <router-link to="/login">Login</router-link>
      <router-link to="/registration">Registration</router-link>
    </div>
  </nav>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  align-items: center;
}

nav {
  padding: 30px;
  align-items: center;
  display: flex;
}
nav a {
  font-weight: bold;
  color: #2c3e50;
  margin-left: 20px;
  text-decoration: none;
}

nav a.router-link-exact-active {
  color: #9418ff;
  text-decoration: underline;
}
</style>
<script setup>
import LoginView from "@/views/LoginView.vue";
  import {ref} from 'vue';
  import axios from 'axios';
import RegistrationView from "@/views/RegistrationView.vue";

  const isLoggedIn = ref(false);

  // Проверка наличия токена в localStorage при загрузке компонента
  if (localStorage.getItem('token')) {
  isLoggedIn.value = true;
}

  const logout = () => {
  localStorage.removeItem('token');
  isLoggedIn.value = false;
};
</script>