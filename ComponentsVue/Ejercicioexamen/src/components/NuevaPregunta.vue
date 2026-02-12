<script setup>

import { ref } from "vue";

const props = defineProps({
    temario: {
        type: Object,
        default: () => { }
    }
});

const emit = defineEmits("agregar-pregunta");

let enunciado = ref("");
let temaElegido = ref("");
let respuesta1 = ref("");
let respuesta2 = ref("");
let respuesta3 = ref("");
let respuesta4 = ref("");
let respuestaCorrecta = ref();

const guardarPregunta = (event) => {
    if (event) {
        event.preventDefault();
    }

    emit("agregar-pregunta", {
        id: (props.temario.preguntas.length + 1),
        tema: temaElegido.value,
        pregunta: enunciado.value,
        correcta: "" + respuestaCorrecta.value,
        _1: "" + respuesta1.value,
        _2: "" + respuesta2.value,
        _3: "" + respuesta3.value,
        _4: "" + respuesta4.value,
    })
    
    enunciado.value = ""
    temaElegido.value = ""
    respuesta1.value = ""
    respuesta2.value = ""
    respuesta3.value = ""
    respuesta4.value = ""
    respuestaCorrecta.value = ""


}

</script>

<template>
    <form id="nuevaPregunta">
        <fieldset>
            <legend>Nueva pregunta</legend>
            <label for="tema" class="nuevaPregLabel"> Tema </label>
            <select id="tema" v-model="temaElegido">
                <option v-for="tema in props.temario.temas" :value=tema.id>{{ tema.nombre }}</option>
            </select>
            <br>
            <label for="pregunta" class="nuevaPregLabel">Enunciado</label>
            <textarea id="pregunta" class="nuevaPreg" rows="10" required v-model="enunciado"></textarea>
            <br>
            <label for="op1" class="nuevaPregLabel">Opción 1</label>
            <input type="text" id="op1" class="nuevaPreg" v-model="respuesta1" required>
            <br>
            <label for="op2" class="nuevaPregLabel">Opción 2</label>
            <input type="text" id="op2" class="nuevaPreg" v-model="respuesta2" required>
            <br>
            <label for="op3" class="nuevaPregLabel">Opción 3</label>
            <input type="text" id="op3" class="nuevaPreg" v-model="respuesta3" required>
            <br>
            <label for="op4" class="nuevaPregLabel">Opción 4</label>
            <input type="text" id="op4" class="nuevaPreg" v-model="respuesta4" required>
            <br>
            <label for="respCorrecta">Respuesta correcta</label>
            <input type="number" id="respCorrecta" min="1" v-model="respuestaCorrecta" max="4" required>
            <input type="submit" value="Guardar" id="guardarPreg" @click="guardarPregunta">
        </fieldset>
    </form>
</template>

<style scoped></style>
