<template>
  <div id="app">
    <div class="cart">Cart {{ cart.length }}</div>
    <ProductDisplay
      :premium="premium"
      @add-to-cart="updateCart"
    ></ProductDisplay>
  </div>
</template>

<script setup lang="ts">
const arrCart: number[] = [];

const cart = ref(arrCart);

const premium = true;

const updateCart = (id: number) => {
  cart.value.push(id);
};
</script>

<style>
.cart {
  float: right;
  border: 2px solid;
  margin: 10px;
  padding: 5px;
}
</style>
