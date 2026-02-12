<script setup>
import { ref } from 'vue';

const props = defineProps({
    temas: {
        type: Array,
        default: () => []
    }
});

const emit = defineEmits("agregar-tema");

let nombreTema = ref("");

const guardarTema = (event) => {
    if (event) {
        event.preventDefault();
    }

    emit("agregar-tema", {
        id: (props.temas.length + 1),
        nombre: nombreTema.value
    })

    nombreTema.value = "";
}

</script>

<template>
    <form id="nuevoTema">
        <fieldset>
            <legend>Nuevo tema</legend>
            <label for="nuevoTemaText">Tema</label>
            <input type="text" id="nuevoTemaText" required v-model="nombreTema" >
            <input type="submit" value="Guardar" id="guardarTema" @click="guardarTema">
        </fieldset>
    </form>
</template>

<style scoped></style>
