<script setup>
import { onMounted, onUnmounted, onActivated, onDeactivated } from 'vue';
import ListaProductos from '../ListaProductos.vue';
import { productos } from '../../data/productos.js';

const productosFiltrados = productos.filter(p => p.categoria === 'Electrónica');

onMounted(()      => console.log('TabElectronica — montado'));
onUnmounted(()    => console.log('TabElectronica — desmontado'));
onActivated(()    => console.log('TabElectronica — activado'));
onDeactivated(()  => console.log('TabElectronica — desactivado'));
</script>

<template>
  <div class="tab-content">
    <h2>Catálogo: Electrónica</h2>
    <ListaProductos :productos="productosFiltrados" />
  </div>
</template>