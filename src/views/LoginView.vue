<template>
  <div class="login">
    <h1>Login</h1>
    <form @submit.prevent="login">
      <div class="log-p">
        <label for="email">Email</label>
        <input type="email" id="email" v-model="email" required />
      </div>

      <div class="log-p">
        <label for="password">Password</label>
        <input type="password" id="password" v-model="password" required />
      </div>

      <button type="submit">Login</button>
    </form>
    <p v-if="error">{{ error }}</p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      email: "",
      password: "",
      error: ""
    };
  },
  methods: {
    async login() {
      try {
        const response = await axios.post("https://jurapro.bhuser.ru/api-shop/login", {
          email: this.email,
          password: this.password
        });
        localStorage.setItem("user", JSON.stringify(response.data));
        this.$router.push("/");
      } catch (error) {
        this.error = "Invalid email or password";
      }
    }
  }
};
</script>

<style>
.login{
  width: 288px;
  height: 250px;
  border-radius: 23px;
  border: 2px solid #8e73bc;
}
.log-p{
  margin-top: 20px;
}
button{
  margin-top: 20px;
}
</style>