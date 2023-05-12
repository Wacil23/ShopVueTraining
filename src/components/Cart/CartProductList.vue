<script setup lang="ts">
import type { ProductCartInterface } from '@/interfaces'
import CartProduct from './CartProduct.vue'

defineProps<{
  cart: ProductCartInterface[]
}>()
const emit = defineEmits<{
  (e: 'deleteProductFromCart', productId: number): void
}>()
</script>

<template>
  <div class="d-flex flex-column">
    <CartProduct v-for="product of cart" :product="product" :key="product.id"  @delete-product-from-cart="emit('deleteProductFromCart', $event)"/>
  </div>
</template>

<style lang="scss" scoped></style>
