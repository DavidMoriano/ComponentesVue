<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
    citas: {
        type: Array,
        default: () => []
    }
})

const diaSeleccionado = ref(null)

const citasDelDia = computed(() => {
    if (!diaSeleccionado.value) return []
    const fechaBuscada = `2021-02-${String(diaSeleccionado.value).padStart(2, '0')}`
    const citaEncontrada = props.citas.find(c => c.fecha === fechaBuscada)
    return citaEncontrada ? citaEncontrada.texto : []
})

const diasConCitas = computed(() => {
    const dias = []
    props.citas.forEach(cita => {
        const dia = Number(cita.fecha.split('-')[2])
        if (dia >= 1 && dia <= 28 && !dias.includes(dia)) {
            dias.push(dia)
        }
    })
    return dias;
});

const diasFebrero = ref([
    [1, 2, 3, 4, 5, 6, 7],
    [8, 9, 10, 11, 12, 13, 14],
    [15, 16, 17, 18, 19, 20, 21],
    [22, 23, 24, 25, 26, 27, 28]
])

const toggleDia = (dia) => {
    diaSeleccionado.value = diaSeleccionado.value === dia ? null : dia
}

const obtenerClaseDia = (dia) => ({
    fondoVerde: dia === diaSeleccionado.value,
    diaConCita: diasConCitas.value.includes(dia)
});

</script>

<template>
    <div class="contendorCalendario">
        <div class="fila-horizontal">
            <div class="calendario">
                <table>
                    <thead>
                        <tr>
                            <th>Lunes</th>
                            <th>Martes</th>
                            <th>Miércoles</th>
                            <th>Jueves</th>
                            <th>Viernes</th>
                            <th>Sábado</th>
                            <th>Domingo</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(semana, index) in diasFebrero" :key="index">
                            <td v-for="dia in semana" :key="dia" :class="obtenerClaseDia(dia)"
                                @dblclick="toggleDia(dia)">
                                {{ dia }}
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <div class="textoCitas">
                <h2>Citas</h2>
                <p v-if="!diaSeleccionado">Selecciona un día del calendario</p>
                <p v-else-if="citasDelDia.length === 0">No hay citas para ese día</p>
                <ul v-else>
                    <li v-for="texto in citasDelDia" :key="texto">
                        {{ texto }}
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<style scoped>
.contendorCalendario {
    display: flex;
    flex-direction: column;
    background-color: rgb(250, 128, 114, 0.4);
    padding: 20px;
    gap: 20px;
    max-width: 1400px;
    margin: 0 auto;
}

.fila-horizontal {
    display: flex;
    flex-direction: row;
    gap: 24px;
    align-items: flex-start;
}

.calendario {
    width: 60%;
    background: white;
    border-radius: 8px;
    padding: 16px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.textoCitas {
    width: 40%;
    background-color: white;
    border-radius: 8px;
    padding: 20px;
    min-height: 320px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

table {
    width: 100%;
    border-collapse: collapse;
}

table,
tr,
th,
td {
    border: 2px solid black;
    text-align: center;
    padding: 12px;
    font-size: 1.1rem;
}

th {
    background-color: #f0f0f0;
    font-weight: bold;
}

.diaConCita {
    color: red;
    font-size: 40px;
}

.fondoVerde {
    background-color: lime;
}
</style>