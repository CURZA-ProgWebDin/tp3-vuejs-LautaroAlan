<script setup>
import { onMounted, onUnmounted, onActivated, onDeactivated } from 'vue';
import ListaProductos from '../ListaProductos.vue';
import { productos } from '../../data/productos.js';

onMounted(()      => console.log('TabTodos — montado'));
onUnmounted(()    => console.log('TabTodos — desmontado'));
onActivated(()    => console.log('TabTodos — activado'));
onDeactivated(()  => console.log('TabTodos — desactivado'));
</script>

<template>
  <div class="tab-content">
    <h2>Todos los productos</h2>
    <ListaProductos :productos="productos" />
  </div>
</template>