<script setup>
import { ref } from 'vue';

const header = ref('App Lista de compras');
const items = ref([]);

const saveItem = () => {
  items.value.push({ id: items.value.length + 1, label: newItem.value });
  newItem.value = '';
};

const newItem = ref('');
const newItemHighPriority = ref(false);
const isNewItemVisible = ref(false); // Inicialmente, la caja de texto está oculta

const showNewItemInput = () => {
  isNewItemVisible.value = true;
};

const hideNewItemInput = () => {
  isNewItemVisible.value = false;
};
</script>

<template>
  <div class="header">
    <h1> <i class="material-icons shopping-cart-icon">local_mall</i> {{ header }}</h1>
    <button class="btn" @click="hideNewItemInput">Cancelar</button>
    <button class="btn btn-primary" @click="showNewItemInput">Agregar articulos</button>
  </div>
  <form v-if="isNewItemVisible" v-on:submit.prevent="saveItem" class="add-item form">
    <!-- Input de Nuevo Articulo -->
    <input v-model.trim="newItem" type="text" placeholder="Ingresar nuevo articulo">
    <!-- Check Boxes -->
    <label>
      <input v-model="newItemHighPriority" type="checkbox">
      Alta Prioridad
    </label>
    {{ newItemHighPriority ? "🔥" : "🧊" }}
    <!-- Boton de UI -->
    <button class="btn btn-primary">Salvar Articulo</button>
  </form>
  <ul>
    <li v-for="{ id, label } in items" v-bind:key="id">
      🔹 {{ label }}
    </li>
  </ul>
  <p v-if="items.length === 0"> 🥀 lista de compras vacía 🥀 </p>
  <p v-else>🔥 ingrese más items </p>
</template>


<style scoped>
.shopping-cart-icon {
  font-size: 2rem; /* Adjust the font-size value as per your desired size */
}
</style>
