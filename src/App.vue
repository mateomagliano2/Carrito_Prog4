<template>
  <div style="font-family: sans-serif; padding: 20px;">
    <h1>Tienda Vue 3</h1>

    <div style="display: flex; gap: 15px; margin-bottom: 30px;">
      <!-- Se pasa cada producto por prop y se escucha el evento "agregar" -->
      <ProductoCard v-for="producto in productos" :key="producto.id" :producto="producto" @agregar="agregarAlCarrito" />
    </div>

    <!-- Se pasa el array del carrito por prop y se escucha el evento "eliminar" -->
    <Carrito :carrito="carrito" @eliminar="eliminarDelCarrito" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import ProductoCard from './components/ProductoCard.vue'
import Carrito from './components/Carrito.vue'

// Array reactivo de productos
const productos = ref([
  { id: 1, nombre: 'Remera', precio: 15000, stock: 5 },
  { id: 2, nombre: 'Pantalón', precio: 25000, stock: 3 },
  { id: 3, nombre: 'Zapatillas', precio: 50000, stock: 2 }
])

// Array reactivo para el carrito
const carrito = ref([])

// Función que se ejecuta al recibir el emit "agregar"
const agregarAlCarrito = (producto) => {
  if (producto.stock > 0) {
    // 1. Restamos el stock del producto original
    producto.stock--

    // 2. Buscamos si ya está en el carrito
    const itemEnCarrito = carrito.value.find(item => item.id === producto.id)

    if (itemEnCarrito) {
      itemEnCarrito.cantidad++
    } else {
      // Si no está, lo agregamos con cantidad 1
      carrito.value.push({ ...producto, cantidad: 1 })
    }
  }
}

// Función que se ejecuta al recibir el emit "eliminar"
const eliminarDelCarrito = (producto) => {
  // 1. Devolvemos el stock al producto original en la tienda
  const productoOriginal = productos.value.find(p => p.id === producto.id)
  if (productoOriginal) {
    productoOriginal.stock += producto.cantidad
  }

  // 2. Lo filtramos (eliminamos) del carrito
  carrito.value = carrito.value.filter(item => item.id !== producto.id)
}
</script>
<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
