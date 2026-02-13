<script setup>
import { computed, ref } from 'vue';

const props = defineProps({
    infoDias: {
        type: Object,
        default: () => {}
    }
});

const emit = defineEmits("agregar-salida");

let nombrePersona = ref(null);
let diaSemanaSeleccionado = ref(null);
let parteDiaSeleccionado = ref(null);

const selectPartesDia = computed (() => {
    return props.infoDias.partesDia;
});

const selectDiasSemana = computed (() => {
    return props.infoDias.diasSemana;
})

const apuntarseSalida = (event) => {
    if (event)
        event.preventDefault();

    emit("agregar-salida", {
        nombre: nombrePersona.value,
        parteDia: parteDiaSeleccionado.value,
        diaSemana: diaSemanaSeleccionado.value
    })

    nombrePersona.value = "";
    parteDiaSeleccionado.value = "";
    diaSemanaSeleccionado.value = "";
}

</script>

<template>
    <fieldset>
        <legend>Formulario</legend>
        <form>
            <label for="nombre">Nombre: </label>
            <input type="text" id="nombre" required v-model="nombrePersona">
            <label for="parteDia"> Parte del día </label>
            <select id="parteDia" v-model="parteDiaSeleccionado">
                <option v-for="(parte, index) in selectPartesDia" :key="index" :value=index>{{ parte }}</option>
            </select>
            <select id="diaSemana" v-model="diaSemanaSeleccionado">
                <option v-for="(dia, index) in selectDiasSemana" :key="index" :value=index>{{ dia }}</option>
            </select>
            <input type="submit" value="Apuntarse" @click="apuntarseSalida">
        </form>
    </fieldset>

</template>

<style scoped>
fieldset {
    border: none;
    padding: 0;
    margin: 2rem 0;
    background: transparent;
}

legend {
    font-size: 1.4rem;
    font-weight: 700;
    color: #111827;
    margin-bottom: 1.5rem;
}

form {
    display: grid;
    gap: 1.2rem;
}

label {
    font-size: 0.9rem;
    font-weight: 500;
    color: #374151;
}

input[type="text"],
select {
    padding: 0.7rem 1rem;
    border: 1px solid #d1d5db;
    border-radius: 6px;
    font-size: 1rem;
}

input[type="text"]:focus,
select:focus {
    border-color: #6366f1;
    outline: none;
    box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.1);
}

input[type="submit"] {
    padding: 0.8rem;
    background: #6366f1;
    color: white;
    border: none;
    border-radius: 6px;
    font-weight: 600;
    cursor: pointer;
}

input[type="submit"]:hover {
    background: #4f46e5;
}
</style>
