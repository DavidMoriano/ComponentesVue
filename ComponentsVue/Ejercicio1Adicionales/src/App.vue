<script setup>
import { ref } from 'vue'
import Calendario from './components/Calendario.vue'
import Formulario from './components/Formulario.vue'

const listaCitas = ref([])

const agregarCita = (nuevaCita) => {
  const existente = listaCitas.value.find(cita => cita.fecha === nuevaCita.fecha)

  if (existente) {
    existente.texto.push(nuevaCita.texto)
  } else {
    listaCitas.value.push({
      fecha: nuevaCita.fecha,
      texto: [nuevaCita.texto]   
    })
  }
}
</script>

<template>
  <Calendario :citas="listaCitas" />
  <Formulario @agregar-cita="agregarCita" />
</template>

<style scoped></style>