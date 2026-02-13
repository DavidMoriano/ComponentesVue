<script setup>
import { computed, ref } from 'vue';
import Formulario from './components/FormularioComponent.vue';
import TablaGrupos from './components/TablaGrupos.vue';

let listaDeSalidas = ref([]);

let informacionSalidas = ref(
  {
    partesDia: ["Mañana", "Tarde", "Noche"],
    diasSemana: ["Lunes", "Martes", "Miércoles", "Jueves", "Viernes", "Sábado", "Domingo"]
  }
)

const agregarSalida = (nuevaSalida) => {
  listaDeSalidas.value.push(nuevaSalida);
  console.log(listaDeSalidas.value);
}

const grupoParaSalidas = computed(() => {
  return listaDeSalidas.value;
});

</script>

<template>
  <Formulario @agregar-salida="agregarSalida" :infoDias="informacionSalidas"></Formulario>
  <TablaGrupos :infoDias="informacionSalidas" :gruposSalidas="grupoParaSalidas"></TablaGrupos>
</template>

<style scoped></style>
