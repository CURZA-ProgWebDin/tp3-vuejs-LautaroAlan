<script setup>
import { onMounted, onUnmounted, onActivated, onDeactivated } from 'vue';
import ListaProductos from '../ListaProductos.vue';
import { productos } from '../../data/productos.js';

const productosFiltrados = productos.filter(p => p.categoria === 'Periféricos');

onMounted(()      => console.log('TabPerifericos — montado'));
onUnmounted(()    => console.log('TabPerifericos — desmontado'));
onActivated(()    => console.log('TabPerifericos — activado'));
onDeactivated(()  => console.log('TabPerifericos — desactivado'));
</script>

<template>
  <div class="tab-content">
    <h2>Catálogo: Periféricos</h2>
    <ListaProductos :productos="productosFiltrados" />
  </div>
</template>