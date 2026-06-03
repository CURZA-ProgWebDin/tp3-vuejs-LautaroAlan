<script setup>
import { ref } from 'vue';


const expandida = ref(false);


const toggleExpandir = () => {
  expandida.value = !expandida.value;
};
</script>

<template>
  <div class="tarjeta">
    <header class="tarjeta-header">
      <slot name="header"></slot>
    </header>

    <main class="tarjeta-body">
      <slot name="body" :expandida="expandida" :toggleExpandir="toggleExpandir"></slot>
    </main>

    <footer class="tarjeta-footer">
      <slot name="footer">
        <span>Sin acciones disponibles</span>
      </slot>
    </footer>
  </div>
</template>

<style scoped>
.tarjeta {
  background: white;
  border: 1px solid #e2e8f0;
  border-radius: 16px;
  padding: 24px;
  display: flex;
  flex-direction: column;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.tarjeta:hover {
  border-color: var(--primary);
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1);
}

.badge-categoria {
  background: #dbeafe;
  color: var(--primary);
  font-size: 0.75rem;
  font-weight: 700;
  padding: 4px 12px;
  border-radius: 99px;
  text-transform: uppercase;
}

.precio {
  font-size: 1.75rem;
  font-weight: 800;
  color: #1e293b;
  margin: 15px 0;
}

.btn-toggle {
  color: var(--primary);
  font-weight: 600;
  cursor: pointer;
  background: none;
  border: none;
  padding: 0;
  font-size: 0.9rem;
}

.btn-comprar {
  background: var(--primary);
  color: white;
  border: none;
  padding: 12px;
  border-radius: 10px;
  font-weight: 700;
  font-size: 1rem;
  cursor: pointer;
  margin-top: 10px;
}

.btn-comprar:hover {
  background: var(--primary-dark);
}
</style>