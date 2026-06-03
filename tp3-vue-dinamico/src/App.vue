<script setup>
import PanelPestanas from './PanelPestanas.vue';
</script>

<template>
  <div id="app-container">
    <h1 class="titulo-principal">Catálogo de Productos - TP3</h1>
    
    <PanelPestanas />
  </div>
</template>

<style>
:root {
  --primary: #1d4ed8; 
  --primary-dark: #1e40af;
  --bg-app: #f1f5f9;
  --text-main: #0f172a;
}

body {
  margin: 0;
  background-color: var(--bg-app);
  color: var(--text-main);
  font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
}

#app-container {
  max-width: 1100px;
  margin: 0 auto;
  padding: 40px 20px;
}

.titulo-principal {
  font-size: 2.2rem;
  font-weight: 800;
  text-align: center;
  margin-bottom: 40px;
  color: var(--text-main);
  text-transform: tight;
}

.tab-content h2 {
  color: #334155;
  font-size: 1.4rem;
  font-weight: 700;
  text-align: center;
  margin-top: 10px;
  margin-bottom: 25px;
  letter-spacing: -0.01em;
}
</style>