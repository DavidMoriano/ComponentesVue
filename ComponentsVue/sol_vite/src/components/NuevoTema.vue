<template>
    <form @submit.prevent="guardarTema">
        <fieldset>
          <legend>Nuevo tema</legend>
            <label for="nombreTema">Tema</label>
            <input id="nombreTema" type="text" v-model="nombreTema" required/>
            <input type="submit" value="Guardar" id="guardarTema"/>
        </fieldset>
    </form>
</template>

<script setup>
import { ref } from "vue";

const emit = defineEmits(["nuevoTema"]);
let nombreTema = ref("");

function guardarTema() {
  if (!nombreTema.value) 
    return;
  emit("nuevoTema", nombreTema.value);
  nombreTema.value = "";
}
</script>
