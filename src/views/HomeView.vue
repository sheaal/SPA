<template>
  <div class="catalog">
    <section v-for="product in this.catalog" class="product-list">
      <div class="product-item">
        <h2 class="product-name">{{ product.name }}</h2>
        <p class="product-info">{{ product.price }} руб</p>
        <p class="product-info">{{ product.description }}</p>
        <button class="prod-but">into a cart</button>
      </div>
    </section>
  </div>
</template>
<style>
.catalog{
  gap: 30px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
.product-list{
  background: #867a9a;
  border-radius: 7px;
  height: 245px;
}
.product-list:hover {
  box-shadow: 2px 4px 10px #9780cb;
}
.prod-but{
  border-radius: 7px;
  background: #c9a9f3;
}
.prod-but:hover {
  box-shadow: 0px 1px 13px #595858;
}
</style>
<script>


import axios from "axios";
export default {
  data() {
    return {
      catalog: []
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
  }
};
</script>