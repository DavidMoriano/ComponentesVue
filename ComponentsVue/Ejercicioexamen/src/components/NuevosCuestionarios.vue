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
            <p>{{ pregunta }}</p>
        </div>
    </div>
</template>

<style scoped></style>
