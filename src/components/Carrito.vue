<template>
  <div style="border: 2px dashed #766; padding: 20px; border-radius: 8px; max-width: 400px;">
    <h2>🛒 Carrito</h2>
    <div v-if="carrito.length === 0">
      <br>
      <p>Agregue un producto al carrito...</p>
    </div>

    <ul v-else style="list-style: none; padding: 0;">
      <li v-for="item in carrito" :key="item.id" style="margin-bottom: 10px;">
        <strong>{{ item.nombre }}</strong> (x{{ item.cantidad }}) ➡️ ${{ item.precio * item.cantidad }}

        <button @click="$emit('eliminar', item)" style="margin-left: 10px; color: red;">
          ❌ ELIMINAR ❌
        </button>
      </li>
    </ul>

    <h3 v-if="carrito.length > 0">Total: ${{ totalCarrito }}</h3>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  carrito: {
    type: Array,
    required: true
  }
})

defineEmits(['eliminar'])

const totalCarrito = computed(() => {
  return props.carrito.reduce((total, item) => total + (item.precio * item.cantidad), 0)
})
</script>
