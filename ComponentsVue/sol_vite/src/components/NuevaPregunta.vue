<template>
    <form @submit.prevent="guardarPregunta">
        <fieldset>
            <legend>Nueva pregunta</legend>
            <label class="nuevaPregLabel">Tema</label>
            <select class="nuevaPreg" v-model.number="temaSeleccionado" required>
                <option disabled value="">Seleccione tema</option>
                <option v-for="tema in temas" :key="tema.id" :value="tema.id">
                    {{ tema.nombre }}
                </option>
            </select>
            <br>
            <label for="pregunta" class="nuevaPregLabel">Enunciado</label>
            <textarea id="pregunta" class="nuevaPreg" rows="10" v-model.trim="enunciado" required></textarea>
            <br>
            <label for="op1" class="nuevaPregLabel">Opción 1</label>
            <input type="text" id="op1" class="nuevaPreg" v-model.trim="opciones[0]" required>
            <br>
            <label for="op2" class="nuevaPregLabel">Opción 2</label>
            <input type="text" id="op2" class="nuevaPreg" v-model.trim="opciones[1]" required>
            <br>
            <label for="op3" class="nuevaPregLabel">Opción 3</label>
            <input type="text" id="op3" class="nuevaPreg" v-model.trim="opciones[2]" required>
            <br>
            <label for="op4" class="nuevaPregLabel">Opción 4</label>
            <input type="text" id="op4" class="nuevaPreg" v-model.trim="opciones[3]" required>
            <br>
            <label for="respCorrecta">Respuesta correcta</label>
            <input type="number" id="respCorrecta" min="1" max="4" v-model.number="correcta" required>
            <input type="submit" value="Guardar" id="guardarPreg">
        </fieldset>
    </form>
</template>

<script setup>
import { ref } from "vue";

defineProps({
  temas: {
    type: Array,
    required: true
  }
});

const emit = defineEmits(["nuevaPregunta"]);

let temaSeleccionado = ref("");
let enunciado = ref("");
let opciones = ref(["", "", "", ""]);
let correcta = ref(null);

function guardarPregunta() {
  if (!temaSeleccionado.value || !enunciado.value || opciones.value.some(o => !o) || !correcta.value) 
    return;

  const nuevaPregunta = {
    id: 0,
    tema: temaSeleccionado.value,
    pregunta: enunciado.value,
    correcta: String(correcta.value),
    _1: opciones.value[0],
    _2: opciones.value[1],
    _3: opciones.value[2],
    _4: opciones.value[3]
  }

  emit("nuevaPregunta", nuevaPregunta);

  temaSeleccionado.value = "";
  enunciado.value = "";
  opciones.value = ["", "", "", ""];
  correcta.value = null;
}
</script>
<style scoped>
.nuevaPreg {
    width: 60%;
}

.nuevaPregLabel {
    display: block;
    width: 20%;
    float: left;
    font-weight: bold;
    text-align: right;
    margin-right: 5px;
}
</style>