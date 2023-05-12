<script setup lang="ts">
import TheCart from './components/Cart/TheCart.vue'
import TheFooter from './components/TheFooter.vue'
import TheHeader from './components/TheHeader.vue'
import TheShop from './components/Shop/TheShop.vue'
import data from './data/product'
import { computed, reactive } from 'vue'
import type { ProductInterface, ProductCartInterface } from './interfaces'

const state = reactive<{
  products: ProductInterface[]
  cart: ProductCartInterface[]
}>({
  products: data,
  cart: []
})

const addProductToCart = (productId: number) => {
  const product = state.products.find((product) => product.id === productId)
  if (product) {
    const productInCart = state.cart.find((product) => product.id === productId)
    if (productInCart) {
      productInCart.quantity++
      return
    }
    else{
      state.cart.push({ ...product, quantity: 1 })
    }
  }
}

const deleteProductFromCart = (productId: number) => {
  const profuctFromCart = state.cart.find((product) => product.id === productId)
  if (profuctFromCart) {
    if (profuctFromCart.quantity > 1) {
      profuctFromCart.quantity--
    }
    else {
      state.cart = state.cart.filter((product) => product.id !== productId)
    }
  }
}
const cartEmpty = computed(() => state.cart.length === 0)
</script>

<template>
  <div class="app-container" :class="{
    gridEmpty : cartEmpty
  }">
    <TheHeader class="header" />
    <TheFooter class="footer" />
    <TheShop :products="state.products" @add-product-to-cart="addProductToCart" class="shop" />
    <TheCart v-if="!cartEmpty" :cart="state.cart" @delete-product-from-cart="deleteProductFromCart" class="cart" />
  </div>
</template>

<style lang="scss">
@import './assets/scss/base.scss';
@import './assets/scss/debug.scss';

.app-container {
  min-height: 100vh;
  display: grid;
  grid-template-areas: 'header header' 'shop cart' 'footer footer';
  grid-template-columns: 75% 25%;
  grid-template-rows: 48px auto 48px;
}

.gridEmpty {
  grid-template-areas: 'header header' 'shop shop' 'footer footer';
  grid-template-columns: 100%;
}

.header {
  grid-area: header;
}

.shop {
  grid-area: shop;
}

.cart {
  grid-area: cart;
  border-left: var(--border);
  background-color: white;
}

.footer {
  grid-area: footer;
}
</style>
