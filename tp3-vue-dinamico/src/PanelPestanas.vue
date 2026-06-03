<script setup>
import { shallowRef, ref } from 'vue';
import TabTodos from './components/tabs/TabTodos.vue';
import TabElectronica from './components/tabs/TabElectronica.vue';
import TabPerifericos from './components/tabs/TabPerifericos.vue';


const tabActivo = shallowRef(TabTodos);


const tabs = {
  'Todos': TabTodos,
  'Electrónica': TabElectronica,
  'Periféricos': TabPerifericos
};

const usarKeepAlive = ref(false);

/*
 * ¿En qué situación conviene usar KeepAlive y en cuál no?
 * * - CONVIENE USARLO: 
 * 1. Cuando los componentes son "pesados" de renderizar y queremos mejorar el rendimiento de navegación.
 * 2. Cuando el componente hace peticiones a una API costosas y no queremos repetir la llamada al cambiar de pestaña.
 * 3. Cuando necesitamos preservar el estado de la UI para el usuario (por ejemplo, si llenó la mitad de un formulario, 
 * o hizo scroll hacia abajo en una lista y queremos que al volver la lista siga en ese mismo lugar).
 * * - NO CONVIENE USARLO:
 * 1. Cuando los datos de esa pestaña necesitan estar estrictamente actualizados cada vez que el usuario ingresa (datos en tiempo real).
 * 2. Si tenemos muchos componentes pesados y cacheados, ya que KeepAlive mantiene las instancias en la memoria RAM del navegador, 
 * pudiendo degradar el rendimiento general de la aplicación por consumo excesivo de memoria.
 */

</script>

<template>
  <div class="panel-container">
    
    <header class="controles">
      <nav class="botones-tabs">
        <button 
          v-for="(componente, nombre) in tabs" 
          :key="nombre"
          @click="tabActivo = componente"
          :class="{ activo: tabActivo === componente }"
        >
          {{ nombre }}
        </button>
      </nav>

      <div class="toggle-keepalive">
        <label>
          <input type="checkbox" v-model="usarKeepAlive">
          Activar caché (KeepAlive)
        </label>
      </div>
    </header>

    <hr>

    <main class="vista-activa">
      
      <KeepAlive v-if="usarKeepAlive">
        <component :is="tabActivo" />
      </KeepAlive>

      <component v-else :is="tabActivo" />

    </main>

  </div>
</template>

<style scoped>
.panel-container {
  background: white;
  border-radius: 12px;
  box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
  padding: 30px;
}

.botones-tabs {
  display: flex;
  gap: 10px;
  background: #f8fafc;
  padding: 6px;
  border-radius: 10px;
  width: fit-content;
}

.botones-tabs button {
  border: none;
  background: transparent;
  padding: 10px 24px;
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s ease;
  color: #64748b;
}

.botones-tabs button.activo {
  background: var(--primary);
  color: white;
  box-shadow: 0 4px 6px -1px rgba(29, 78, 216, 0.3);
}

.toggle-keepalive {
  margin-top: 15px;
  font-size: 0.9rem;
  font-weight: 500;
  color: #475569;
}
</style>