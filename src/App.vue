<template>
  <div v-for="personaje in personajesArray" :key="personaje.id">
    <p>Nombre: {{personaje.name}}</p>
    <p>especie: {{personaje.species}}</p>
    <p>Origen: {{personaje.origin.name}}</p>
    <button v-on:click="eliminar(personaje.id)">Eliminar</button>
  </div>
      <button v-on:click="agregar()">HELP ME!!!!</button>

</template>

<script setup>
import axios from "axios";
import {ref, onMounted} from "vue";
  const personajesArray = ref([]);
  const eliminar = id => {
    personajesArray.value = personajesArray.value.filter((personaje) => personaje.id !== id);
  }
  const agregar = () => {
    const personajeNuevo = {
      name: "personaje xd",
      id: "1",
      origin: {
        name: "Nose"
      },
      species: "Yes",
    }
    personajesArray.value.push(personajeNuevo);
  }

onMounted(() => {
  axios("https://rickandmortyapi.com/api/character").then(res => {
    personajesArray.value = res.data.results;
    console.log(personajesArray);
});
})
</script>

<style>

</style>
