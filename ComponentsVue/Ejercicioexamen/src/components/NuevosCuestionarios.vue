<script setup>
import { computed } from 'vue';

const props = defineProps({
    cuestionarios: {
        type: Object,
        default: () => { }
    }
});

const mostrarCuestionario = computed(() => {
    return props.cuestionarios;
});

</script>

<template>
    <div id="cuestionario">
        <div v-for="pregunta in mostrarCuestionario">
            <p>{{ pregunta.pregunta }}</p>
            <ul>
                <li> <input type="checkbox" name="" id=""></input> {{ pregunta._1 }} </li>
                <li> <input type="checkbox" name="" id=""></input> {{ pregunta._2 }}</li>
                <li> <input type="checkbox" name="" id=""></input> {{ pregunta._3 }}</li>
                <li> <input type="checkbox" name="" id=""></input> {{ pregunta._4 }}</li>
            </ul>
        </div>
    </div>
</template>

<style scoped>
    li {
        list-style: none;
    }
</style>
