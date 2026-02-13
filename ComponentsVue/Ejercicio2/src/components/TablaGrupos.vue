<script setup>
import { computed } from 'vue'

const props = defineProps({
    gruposSalidas: {
        type: Array,
        default: () => []
    },
    infoDias: {
        type: Object,
        default: () => ({})
    }
})

const filasTabla = computed(() => {
    const resultado = [];

    props.gruposSalidas.forEach(salida => {
        const diaIdx = Number(salida.diaSemana);
        const parteIdx = Number(salida.parteDia);

        const diaNombre = props.infoDias.diasSemana[diaIdx];
        const franjaNombre = props.infoDias.partesDia[parteIdx];

        const clave = `${diaIdx}-${parteIdx}`;

        let grupo = resultado.find(g => g.clave === clave);

        if (!grupo) {
            grupo = {
                clave,
                dia: diaNombre,
                franja: franjaNombre,
                participantes: []
            }
            resultado.push(grupo)
        }

        if (!grupo.participantes.includes(salida.nombre)) {
            grupo.participantes.push(salida.nombre)
        }
    })
    return resultado
})
</script>

<template>
    <div class="contenedor-tabla">
        <h1>Tabla de grupos</h1>

        <table>
            <thead>
                <tr>
                    <th>Grupo</th>
                    <th>Día</th>
                    <th>Franja</th>
                    <th>Participantes</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(grupo, idx) in filasTabla" :key="grupo.clave">
                    <td>{{ idx + 1 }}</td>
                    <td>{{ grupo.dia }}</td>
                    <td>{{ grupo.franja }}</td>
                    <td class="participantes">
                        <template v-if="grupo.participantes.length">
                            <span v-for="(nombre, i) in grupo.participantes" :key="nombre">
                                {{ nombre }}
                                <span v-if="i < grupo.participantes.length - 1">, </span>
                            </span>
                        </template>
                        <span v-else class="sin-personas">—</span>
                    </td>
                </tr>

                <tr v-if="!filasTabla.length" class="fila-vacia">
                    <td colspan="4">No hay salidas registradas</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<style scoped>
.contenedor-tabla {
    max-width: 900px;
    margin: 2rem auto;
    padding: 0 1rem;
}

table {
    width: 100%;
    border-collapse: collapse;
    background: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}

th,
td {
    padding: 12px 16px;
    text-align: left;
    border-bottom: 1px solid #e2e8f0;
}

th {
    background: #f8fafc;
    font-weight: 600;
    color: #1e293b;
}

tr:hover {
    background: #f1f5f9;
}

.participantes {
    line-height: 1.5;
}

.sin-personas {
    color: #94a3b8;
}

.fila-vacia td {
    text-align: center;
    padding: 2.5rem;
    color: #64748b;
    background: #f8fafc;
}
</style>