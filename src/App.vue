<script>
import { computed, ref, reactive, toRef, toRefs, watch, watchEffect } from 'vue'

export default {
  setup () {
    const item = reactive({
      name: "Product 1",
      price: 10,
      quantity: 1
    })

    const increment = () => item.quantity++

    const decrement = () => item.quantity--

    const swapProduct = () => {
      item.name = "Product A"
      item.price = 30
    }

    const total = computed(() => item.price * item.quantity)

    const { name, price, quantity } = toRefs(item)

    watch(() => item.quantity, (newValue, oldValue) => {
      if (item.quantity === 5) {
        alert("you cannot add more items")
      }
    }, { immediate: true })

    watchEffect(() => {
      console.log('Price changed: ', item.price)
    })

    return {
      quantity,
      increment,
      decrement,
      name,
      price,
      total,
      swapProduct
    }
  }
}
</script>

<template>
  <h1>{{ name }} : {{ price }}</h1>
  <button @click="swapProduct">Swap product</button>
  <button @click="price++">Increment price</button>

  <h2>{{ quantity }}</h2>
  <button @click="increment">+</button>
  <button @click="decrement">-</button>

  <h3>Total: {{ total }}</h3>
</template>

<style scoped>
</style>