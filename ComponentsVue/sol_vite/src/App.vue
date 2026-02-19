<template>
  <div>
    <header>
      <h1>Generador de test de películas míticas</h1>
    </header>

    <main>
      <section id="formularios">
        <NuevoCuestionario :temas="temas" @generarNuevoCuest="generarCuestionario"/>
        <NuevoTema @nuevoTema="guardarTemaNuevo"/>
        <NuevaPregunta :temas="temas" @nuevaPregunta="guardarNuevaPregunta"/>
      </section>
      <CuestionarioGenerado :preguntas="preguntasParaCuestionario"/>
    </main>
  </div>
</template>

<script setup>
import { ref } from "vue";

import NuevoCuestionario from "./components/NuevoCuestionario.vue";
import NuevaPregunta from "./components/NuevaPregunta.vue";
import NuevoTema from "./components/NuevoTema.vue";
import CuestionarioGenerado from "./components/CuestionarioGenerado.vue";


let temas = ref([
  { id: 1, nombre: "Star Wars" },
  { id: 2, nombre: "Regreso al futuro" },
  { id: 3, nombre: "El señor de los anillos" },
]);
let preguntas = ref([
  {
    id: 1,
    tema: 1,
    pregunta: "¿En qué año se estrenó la primera película de la saga?",
    correcta: "3",
    _1: "1965",
    _2: "1968",
    _3: "1977",
    _4: "1979",
  },
  {
    id: 2,
    tema: 1,
    pregunta: "¿Cuál es la frase más famosa del personaje de Darth Vader?",
    correcta: "4",
    _1: "Me ha fallado por última vez, almirante",
    _2: "Su falta de fe me resulta perturbadora",
    _3: "Ese nombre ya no significa nada para mí",
    _4: "No, yo soy tu padre",
  },
  {
    id: 3,
    tema: 1,
    pregunta: "¿Cómo se llama la primera jedi protagonista?",
    correcta: "2",
    _1: "Elaine",
    _2: "Rey",
    _3: "Hodor",
    _4: "Leia",
  },
  {
    id: 4,
    tema: 3,
    pregunta: "¿Cuál es la criatura que lleva más tiempo viviendo en la Tierra Media?",
    correcta: "3",
    _1: "Gandalf",
    _2: "El Balrog",
    _3: "Tom Bombadil",
    _4: "Sauron",
  },
  {
    id: 5,
    tema: 3,
    pregunta: "En la película, ¿quién pronunció en el Concilio de Elrond la siguiente frase: “os hace falta gente inteligente para este tipo de... misión... cometido... cosa”?",
    correcta: "2",
    _1: "Merry",
    _2: "Pippin",
    _3: "Sam",
    _4: "Gimpli",
  },
  {
    id: 6,
    tema: 3,
    pregunta: "¿Dónde está Gandalf cuando el Nazgûl persigue a los Hobbits en la frontera de la comarca?",
    correcta: "1",
    _1: "En la Torre de Orthanc",
    _2: "En Rivendel",
    _3: "En las Colinas del Viento",
    _4: "En Bree",
  },
  {
    id: 7,
    tema: 2,
    pregunta: "¿Qué modelo es el auto donde Marty y Doc viajan en el tiempo?",
    correcta: "2",
    _1: "Mustang",
    _2: "Delorean",
    _3: "Honda",
    _4: "Tesla",
  },
  {
    id: 8,
    tema: 2,
    pregunta: "¿A qué fecha retrocede Marty accidentalmente?",
    correcta: "2",
    _1: "12 de noviembre de 1975",
    _2: "5 de noviembre de 1955",
    _3: "25 de noviembre de 1965",
    _4: "5 de diciembre de 1955",
  },
  {
    id: 9,
    tema: 2,
    pregunta: "Cuando Marty viaja al pasado y se encuentra con su madre de joven, ¿cómo le dice que se llama?",
    correcta: "3",
    _1: "David",
    _2: "Bob",
    _3: "Calvin",
    _4: "Clint",
  },
  {
    id: 10,
    tema: 2,
    pregunta: "¿Qué canción tocaba McFly en el baile de instituto de la película?",
    correcta: "4",
    _1: "Suspicius mind – Elvis Presley",
    _2: "Hey Jude - The Beatles",
    _3: "Sitting on the dock of the bay Otis Redding",
    _4: "Chuck Berry – Johnny B. Goode",
  },
]);
let preguntasParaCuestionario = ref([]);


function generarCuestionario(idTema, numPreguntas) {
  const preguntasDelTema = preguntas.value.filter(p => p.tema === idTema);
  preguntasParaCuestionario.value = preguntasDelTema.slice(0, numPreguntas);
}

function guardarTemaNuevo(nombreTema) {
  if (!nombreTema) 
    return;

  const existe = temas.value.some( t => t.nombre.toLowerCase() === nombreTema.toLowerCase());

  if (existe) 
    return;

  temas.value.push({
    id: temas.value.length,
    nombre: nombreTema
  });
}

function guardarNuevaPregunta(preguntaNueva) {
  preguntaNueva.id = preguntas.value.length + 1;
  preguntas.value.push(preguntaNueva);
}
</script>

<style>
@import url(//db.onlinewebfonts.com/c/b51d30fb7966b76c8820e214edca3d6b?family=Back+ttf);

header {
  text-align: center;
  font-family: "Back ttf";
  font-size: xx-large;
  color: gold;
}

main {
  display: flex;
}

#formularios {
    float: left;
    width: 40%;
    border-right: 2px dashed gold;
    box-sizing: content-box;
    padding: 5px;
}

#cuestionario {
    float: right;
    width: 45%;
    margin-left: 2%;
    padding-left: 10%;
    border-left: 2px dashed gold;
    box-sizing: content-box;
}

input, select, textarea {
  margin: 3px;
  padding: 2px;
}

fieldset {
  margin-bottom: 15px;
  border-radius: 2em 2em;
  padding-left: 20px;
}
</style>