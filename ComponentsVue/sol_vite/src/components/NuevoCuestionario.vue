<template>
  <fieldset>
    <legend>Generar nuevo cuestionario</legend>
    <form @submit.prevent="generarNuevoCuestionario">
      <label for="numPreguntas">Nº de preguntas</label>
      <input type="number" id="numPreguntas" min="1" v-model.number="numPreguntas" required/>
      <br>
      <label for="temas">Temas</label>
      <select id="temas" v-model.number="temaSeleccionado">
        <option v-for="tema in temas" :key="tema.id" :value="tema.id">
          {{ tema.nombre }}
        </option>
      </select>
      <input type="submit" value="Generar" />
    </form>
  </fieldset>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  temas: {
    type: Array,
    required: true
  }
});
const emit = defineEmits(["generarNuevoCuest"]);
let numPreguntas = ref(1);
let temaSeleccionado = ref(null);

function generarNuevoCuestionario() {
  if (!temaSeleccionado.value) 
    return;
  emit("generarNuevoCuest",temaSeleccionado.value, numPreguntas.value);
}
</script>