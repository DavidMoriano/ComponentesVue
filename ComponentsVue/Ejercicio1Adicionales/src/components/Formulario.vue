<script setup>
import { ref } from "vue"

const emit = defineEmits(["agregar-cita"]);

const fecha = ref("");
const cita = ref("");

const guardarCita = () => {
    if (!fecha.value || !cita.value) return
    emit("agregar-cita", {
        fecha: fecha.value,
        texto: cita.value
    })

    cita.value = "";
}

</script>

<template>
    <div>
        <form action="#">
            <input type="date" v-model="fecha" min="2021-02-01" max="2021-02-28">
            <input type="text" v-model="cita" maxlength="75">
            <button type="button" @click="guardarCita">Almacenar cita</button>
        </form>
    </div>
</template>

<style scoped>
div {
    background: white;
    border-radius: 8px;
    padding: 20px 24px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    margin-top: 16px;
}

form {
    display: flex;
    gap: 16px;
    align-items: center;
}

input[type="date"],
input[type="text"] {
    padding: 10px 12px;
    border: 1px solid #d0d0d0;
    border-radius: 6px;
    font-size: 1rem;
    min-width: 160px;
}

input[type="date"] {
    color: #333;
}

input[type="text"] {
    flex: 1;
    min-width: 280px;
}

input:focus {
    outline: none;
    border-color: #e67e22;
    box-shadow: 0 0 0 3px rgba(230, 126, 34, 0.12);
}

button {
    background-color: #e67e22;
    color: white;
    border: none;
    border-radius: 6px;
    padding: 10px 28px;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: background-color 0.2s;
    white-space: nowrap;
}

button:hover {
    background-color: #d35400;
}
</style>