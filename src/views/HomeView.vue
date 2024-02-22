<template>
  <div class="catalog">
    <section v-for="product in this.catalog" class="product-list">
      <div class="product-item">
        <h2 class="product-name">{{ product.name }}</h2>
        <p class="product-info">{{ product.price }} руб</p>
        <p class="product-info">{{ product.description }}</p>
      </div>
      <button class="prod-but" @click="addToCart(product)">into a cart</button>
    </section>
  </div>
  <CartView :cart="cart"/>
</template>

<script>
import axios from "axios";
import CartView from "./CartView.vue";
// import { mapState } from 'vuex';
export default {
  components: {
    CartView
  },
  // computed: {
  //   ...mapState(['cart'])
  // },
  data() {
    return {
      catalog: [],
      // cart: {}
      registrationData: {
        name: '',
        email: '',
        password: ''
      },
      loginData: {
        email: '',
        password: ''
      }
    };
  },
  async mounted() {
    try {
      const response = await axios.get("https://jurapro.bhuser.ru/api-shop/products");
      this.catalog = response.data.data;
      console.log(this.catalog);
    } catch (error) {
      console.error("Error fetching products:", error);
    }
  },
  methods: {
    addToCart(product) {
      this.$emit('add-to-cart', product);
    },
  },

  // async registerUser() {
  //   try {
  //     const response = await axios.post('https://jurapro.bhuser.ru/api-shop/register', this.registrationData);
  //     console.log('User registered:', response.data);
  //   } catch (error) {
  //     console.error('Error registering user:', error);
  //   }
  // },
  //
  // async loginUser() {
  //   try {
  //     const response = await axios.post('https://jurapro.bhuser.ru/api-shop/login', this.loginData);
  //     console.log('User logged in:', response.data);
  //   } catch (error) {
  //     console.error('Error logging in:', error);
  //   }
  // },

};
</script>

<style>
.catalog{
  margin-top: 30px;
  gap: 30px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
.product-list{
  border: 3px solid #f2ecfb;
  border-radius: 7px;
  height: 265px;
}
.product-list:hover {
  box-shadow: 2px 4px 10px #9780cb;
}
.prod-but{
  border-radius: 7px;
  background: #c9a9f3;
  margin-bottom: 20px;
}
.prod-but:hover {
  box-shadow: 0px 1px 13px #595858;
}
</style>