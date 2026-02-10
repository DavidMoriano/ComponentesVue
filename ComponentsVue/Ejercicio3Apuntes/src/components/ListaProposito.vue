<script setup>
import "../assets/main.css";
import { computed } from 'vue';
const props = defineProps(["propositosListaPropositos"]);
const emit = defineEmits(["agregar-proposito", "cambiarAHecho"]);

function propositoHecho(index) {
    emit("cambiarAHecho", index);
}

const listaPropositosHechos = computed(() => {
    return props.propositosListaPropositos.filter(p => p.hecho === true);
});
</script>

<template>
    <div class="contenedor-principal">
        <h2>Lista de propósitos</h2>

        <div class="contenedor" v-if="propositosListaPropositos.length > 0">
            <div class="layout-paralelo">
                <div class="columna lista">
                    <ul>
                        <li v-for="(proposito, index) in propositosListaPropositos" :key="index">
                            <label>
                                <input type="checkbox" :checked="proposito.hecho" @change="propositoHecho(index)" />
                                <span :class="{ tachado: proposito.hecho }">
                                    {{ proposito.texto }}
                                </span>
                            </label>
                        </li>
                    </ul>
                </div>

                <div class="columna tabla">
                    <table v-if="listaPropositosHechos.length > 0">
                        <tr>
                            <th>Nombre</th>
                            <th>Hecho</th>
                        </tr>
                        <tr v-for="(proposito, index) in listaPropositosHechos" :key="index">
                            <td>{{ proposito.texto }}</td>
                            <td class="fondoVerde"></td>
                        </tr>
                    </table>
                    <p v-else>No hay ningún propósito hecho en la tabla</p>
                </div>
            </div>
        </div>

        <div v-else class="sin-contenido">
            <p>No hay propósitos</p>
        </div>
    </div>
</template>
