<script setup>
import { ref, computed } from 'vue';

const props = defineProps({
    temas: {
        type: Array,
        default: () => []
    }
});

let numeroPreguntas = ref("");
let temaElegido = ref("");

const emit = defineEmits("agregar-cuestionario");

const temasAElegir = computed(() => {
    return props.temas;
})

const generarCuestionario = (event) => {
    if (event) {
        event.preventDefault();
    }

    emit("agregar-cuestionario", {
        preguntas: numeroPreguntas.value,
        temaElegido: temaElegido.value
    })

    temaElegido.value = "";
}

</script>
<template>
    <fieldset>
        <legend>Generar nuevo cuestionario</legend>
        <form id="nuevoTest">
            <label for="numPreguntas">Nº de preguntas</label>
            <input type="number" id="numPreguntas" min="1" required v-model="numeroPreguntas"><br>
            <label for="temas"> Temas </label>
            <select id="temas" v-model="temaElegido">
                <option v-for="tema in temasAElegir" :value=tema.id>{{ tema.nombre }}</option>
            </select>
            <input type="submit" value="Generar" @click="generarCuestionario">
        </form>
    </fieldset>
</template>

<style scoped></style>
