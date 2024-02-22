<template>
  <div class="registration">
    <h2>Registration</h2>
    <form @submit.prevent="register">
      <div class="reg-p">
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="name" required>
      </div>

      <div class="reg-p">
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="email" required>
      </div>

      <div class="reg-p">
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="password" required>
      </div>

      <button type="submit">Sign up</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      name: "",
      email: "",
      password: ""
    };
  },
  methods: {
    async register() {
      try {
        const response = await axios.post("https://jurapro.bhuser.ru/api-shop/signup", {
          name: this.name,
          email: this.email,
          password: this.password
        });
        console.log("User registered:", response.data);
        localStorage.setItem("token", response.data.token); // Сохраняем токен в локальном хранилище
        this.$router.push("/"); // Перенаправляем пользователя на главную страницу
      } catch (error) {
        console.error("Error registering user:", error);
        this.error = "Invalid email or password";
      }
    }
  }
};
</script>

<style>
.registration{
  width: 288px;
  height: 250px;
  border-radius: 23px;
  border: 2px solid #8e73bc;
}
.reg-p{
  margin-top: 20px;
}
button{
  margin-top: 20px;
}
</style>