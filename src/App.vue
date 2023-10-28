<script setup>
import { ref } from 'vue';
const header = ref('App Lista de compras');
const items = ref([
  { id: 1, label: '10 bolillos', purchased: true, highPriority: false },
  { id: 2, label: '1 lata de frijoles', purchased: false, highPriority: true },
  { id: 3, label: '2 lata de atún', purchased: true, highPriority: true }
]);
//funcion que alterna el estado de comprado de newItems
const togglePurchased = (item) =>{
  //invertir la propiedad toggle
  item.purchased = !item.purchased;
}
const saveItem = () => {
  items.value.push({ id: items.value.length + 1, label: newItem.value })
  //Limpiando el contenido de newItem
  newItem.value = ""; 
};
const newItem = ref('');
const newItemHighPriority = ref(false);
const editing = ref(false);
const doEdit = (edit) => {
  //alteramos la variable esditing
  editing.value = edit;
  // limpiamos el input de texto
  newItem.value = ""; 
};
</script>

<template>
  <div class="header">
    <h1> <i class="material-icons shopping-cart-icon">local_mall</i> {{ header }}</h1>
    <button v-if="!editing" @click="doEdit(true)" class="btn btn-primary">Agregar</button>
    <button v-else @click="doEdit(false)" class="btn btn-cancel">Cancelar</button>
  </div>
  
  <!-- <a v-bind:href="newItem">
    <i class="material-icons shopping-cart-icon">link</i>
  </a> -->

  <form v-if="editing" v-on:submit.prevent= saveItem class="add-item form">
    <!-- Input de nuevo articulo -->
    <input class="addint" v-model.trim="newItem" type="text" placeholder="Ingresar articulo">
    <!-- Check Boxes -->
    <label>
      <input v-model="newItemHighPriority" type="checkbox"> Alta Prioridad
    </label>
    {{ newItemHighPriority ? "🔥" : "🧊" }}
    <!-- boton en la UI -->
    <button :disabled="newItem.length === 0" class="btn btn-primary">Salvar articulo</button>
  </form>
  <ul>
    <li v-for="({ id, label, purchased, highPriority }, index) in items" 
    v-bind:key="id"
    :class="{strikeout : purchased, priority: highPriority}"
    @click="togglePurchased(items[index])"
    >   
     <!--otra forma es    :class="[purchased?'strikeout':'']" -->
      🔹 {{ label }}
    </li>
  </ul>
  <p  v-if ="items.length === 0">🥀 Lista de Compras Vacia 🥀</p>
  <p v-else > 🔥 Ingrese más Items</p>
</template>



