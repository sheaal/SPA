<script>
export default {
  props: {
    cart: {
      type: Array,
      required: true
    }
  }
};
</script>

<template>
  <div class="cart">
    <h2>Корзина</h2>
    <ul>
      <li v-for="product in cart" :key="product.id">
        {{ product.name }} - {{ product.price }} руб
      </li>
    </ul>
  </div>
</template>

<style>
.cart {
  background: #867a9a;
  padding: 10px;
}
</style>