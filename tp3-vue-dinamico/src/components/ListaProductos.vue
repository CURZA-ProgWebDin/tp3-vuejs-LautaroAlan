<script setup>
import { ref, useTemplateRef, onMounted, onUpdated, onBeforeUnmount } from 'vue';
import TarjetaProducto from './TarjetaProducto.vue';


const props = defineProps({
  productos: {
    type: Array,
    required: true
  }
});

const box = useTemplateRef('box');

const cargando = ref(false);
let timer = null;

function esperar(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function cargarProductos() {
  cargando.value = true;
  await esperar(800);
  cargando.value = false;
}


onMounted(() => {
  cargarProductos();
  
  timer = setInterval(() => {
    console.log('Ejecutando polling simulado...');
    cargarProductos();
  }, 30000);
});

onUpdated(() => {
  if (box.value) {
    box.value.scrollTop = box.value.scrollHeight;
  }
});

onBeforeUnmount(() => {
  clearInterval(timer);
  console.log('ListaProductos desmontado — polling detenido');
});
</script>

<template>
  <div class="lista-container">
    
    <div v-if="cargando" class="mensaje-carga">
      <h3>Cargando productos...</h3>
    </div>

    <div ref="box" class="lista">
      
      <TarjetaProducto 
        v-for="producto in productos" 
        :key="producto.id"
      >
        <template #header>
          <h4>{{ producto.nombre }}</h4>
          <span class="badge-categoria">{{ producto.categoria }}</span>
        </template>
        
        <template #body="{ expandida, toggleExpandir }">
          <p class="precio">${{ producto.precio }}</p>
          <button @click="toggleExpandir" class="btn-toggle">
            {{ expandida ? 'Ocultar stock' : 'Ver stock' }}
          </button>
          <p v-if="expandida" class="stock">
            Unidades disponibles: {{ producto.stock }}
          </p>
        </template>

        <template #footer>
          <button class="btn-comprar">Agregar</button>
        </template>
      </TarjetaProducto>

    </div>
  </div>
</template>

<style scoped>
.lista-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.mensaje-carga {
  color: #007bff;
  font-weight: bold;
}

.lista {
  max-height: 500px;
  overflow-y: auto;
  border: 1px solid #ddd;
  padding: 1rem;
  border-radius: 8px;
  background-color: #fafafa;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.badge-categoria {
  background-color: #e9ecef;
  padding: 0.2rem 0.5rem;
  border-radius: 4px;
  font-size: 0.8rem;
  color: #495057;
}

.precio {
  font-size: 1.2rem;
  font-weight: bold;
  color: #28a745;
}

.btn-toggle {
  background: none;
  border: none;
  color: #007bff;
  text-decoration: underline;
  cursor: pointer;
  padding: 0;
}

.stock {
  margin-top: 0.5rem;
  color: #dc3545;
  font-size: 0.9rem;
}

.btn-comprar {
  background-color: #0d6efd;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
  width: 100%;
}

.btn-comprar:hover {
  background-color: #0b5ed7;
}

.lista {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
  max-height: 600px;
  overflow-y: auto;
  padding: 10px;
  scrollbar-width: thin;
  scrollbar-color: #cbd5e1 transparent;
}
</style>