<template>
  <div style="border: 1px solid #ccc; padding: 15px; border-radius: 8px; width: 150px;">
    <h3>{{ producto.nombre }}</h3>
    <p>${{ producto.precio }}</p>
    <p>Stock: {{ producto.stock }}</p>

    <!-- Deshabilitamos el botón si no hay stock -->
    <button :disabled="producto.stock === 0" @click="$emit('agregar', producto)">
      {{ producto.stock > 0 ? 'Agregar al carrito' : 'Sin stock' }}
    </button>
  </div>
</template>

<script setup>
// Definimos las props que recibe el componente
defineProps({
  producto: {
    type: Object,
    required: true
  }
})

// Declaramos los eventos que este componente va a emitir hacia arriba
defineEmits(['agregar'])
</script>
