<template>
  <div style="border: 1px solid #ccc; padding: 15px; border-radius: 8px; width: 150px;">
    <h3>{{ producto.nombre }}</h3>
    <p>${{ producto.precio }}</p>
    <p>Stock: {{ producto.stock }}</p>

    <button :disabled="producto.stock === 0" @click="$emit('agregar', producto)" style=" color: darkgreen;">
      {{ producto.stock > 0 ? 'Agregar al carrito' : 'Sin stock' }}
    </button>
  </div>
</template>
<script setup>

defineProps({
  producto: {
    type: Object,
    required: true
  }
})

defineEmits(['agregar'])
</script>
