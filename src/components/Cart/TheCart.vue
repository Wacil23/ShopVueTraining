<script setup lang="ts">
import type { ProductCartInterface } from '@/interfaces'
import CartProductList from './CartProductList.vue'
import { computed } from 'vue'

const props = defineProps<{
  cart: ProductCartInterface[]
}>()

const totalPrice = computed(() => props.cart.reduce((acc, product) => {
  return acc + product.price * product.quantity
}, 0))

const emit = defineEmits<{
  (e: 'deleteProductFromCart', productId: number): void
}>()
</script>

<template>
  <div class="p-20 d-flex flex-column">
    <h2 class="mb-10">Panier</h2>
    <CartProductList
      class="flex-fill"
      :cart="cart"
      @delete-product-from-cart="emit('deleteProductFromCart', $event)"
    />
    <button class="btn btn-success">Commander {{ totalPrice.toFixed(2) }}€</button>
  </div>
</template>

<style lang="scss" scoped></style>
