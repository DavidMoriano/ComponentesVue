<template>
  <section id="cuestionario">
    <div v-if="preguntas.length === 0">
      No hay preguntas disponibles para este tema.
    </div>
    <div v-else>
        <div v-for="pregunta in preguntas" :key="pregunta.id">
        <p> {{ pregunta.pregunta }} </p>
        <div v-for="n in 4" :key="n">
          <input type="radio" :name="'pregunta_' + pregunta.id" :value="n"/>
            {{ pregunta['_' + n] }}
        </div>
        <hr>
      </div>
    </div>
  </section>
</template>

<script setup>
defineProps({
  preguntas: {
    type: Array,
    required: true
  }
})
</script>
