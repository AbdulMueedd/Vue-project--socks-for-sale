<script setup>
import { ref, computed } from 'vue'
import ProductDisplay from '@/components/ProductDisplay.vue'

const cart = ref([])
const premium = ref(true)

const pricePerSock = 9.99

const cartTotal = computed(() => cart.value.length * pricePerSock)
const cartTotalFormatted = computed(() => cartTotal.value.toFixed(2))

const updateCart = (id) => {
  cart.value.push(id)
}

const removeFromCart = () => {
  if (cart.value.length > 0) cart.value.pop()
}
</script>

  
<template>
  <div class="nav-bar"></div>

  <div class="cart">
    Cart({{ cart.length }}) — Total: ${{ cartTotalFormatted }}
    <button :disabled="cart.length === 0" @click="removeFromCart">Remove</button>
  </div>

  <ProductDisplay
    :premium="premium"
    :cart-total="cartTotal"
    @add-to-cart="updateCart"
  />
</template>
