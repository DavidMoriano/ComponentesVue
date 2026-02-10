<script setup>
import ListaProposito from "./components/ListaProposito.vue";
import NuevoProposito from "./components/NuevoProposito.vue";
import "./assets/main.css";

import { ref } from "vue";

const listaPropositos = ref([
  { texto: "Hacer deporte", hecho: false },
  { texto: "Estudiar", hecho: true }
]);

function agregarProposito(nuevo) {
  if (nuevo.texto?.trim()) {
    listaPropositos.value.push(nuevo);
  }
}

function eliminarUltimoProposito() {
  if (listaPropositos.value.length > 0) {
    listaPropositos.value.pop();
  }
}

function borrarLista() {
  listaPropositos.value = [];
}

function cambiarAHecho(index) {
  listaPropositos.value[index].hecho = !listaPropositos.value[index].hecho;
}
</script>

<template>
  <div class="contenedor-principal">
    <h1>Propósitos de año nuevo</h1>

    <NuevoProposito @agregar-proposito="agregarProposito" @eliminar-ultimo-proposito="eliminarUltimoProposito" />

    <ListaProposito :propositos-lista-propositos="listaPropositos" @cambiar-a-hecho="cambiarAHecho" />

    <div class="acciones">
      <button type="button" @click="borrarLista" class="btn borrar" :disabled="listaPropositos.length === 0">
        Borrar toda la lista
      </button>
    </div>
  </div>
</template>