<script setup>
import "../assets/main.css";

import { ref } from "vue";

const nuevoProposito = ref("");

const emit = defineEmits([
    "agregar-proposito",
    "eliminar-ultimo-proposito"
]);

function guardarProposito() {
    if (!nuevoProposito.value.trim()) return;

    emit("agregar-proposito", {
        texto: nuevoProposito.value.trim(),
        hecho: false
    });
    nuevoProposito.value = "";
}

function eliminarUltimoProposito() {
    emit("eliminar-ultimo-proposito");
}
</script>

<template>
    <div class="contenedor-principal">
        <h2>Añadir nuevo propósito</h2>

        <div class="formulario">
            <input type="text" placeholder="Escribe tu nuevo propósito..." v-model="nuevoProposito"
                @keydown.enter="guardarProposito" class="input-proposito" />

            <div class="botones">
                <button @click="guardarProposito" class="btn agregar">
                    Agregar
                </button>

                <button @click="eliminarUltimoProposito" class="btn eliminar">
                    Eliminar último
                </button>
            </div>
        </div>
    </div>
</template>
