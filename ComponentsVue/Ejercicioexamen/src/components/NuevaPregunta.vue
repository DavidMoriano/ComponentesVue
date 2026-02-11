<script setup></script>

<template>
    <form id="nuevaPregunta">
        <fieldset>
            <legend>Nueva pregunta</legend>
            <label for="tema" class="nuevaPregLabel"> Tema </label>
            <select id="tema" class="nuevaPreg">
            </select>
            <br>
            <label for="pregunta" class="nuevaPregLabel">Enunciado</label>
            <textarea id="pregunta" class="nuevaPreg" rows="10" required></textarea>
            <br>
            <label for="op1" class="nuevaPregLabel">Opción 1</label>
            <input type="text" id="op1" class="nuevaPreg" required>
            <br>
            <label for="op2" class="nuevaPregLabel">Opción 2</label>
            <input type="text" id="op2" class="nuevaPreg" required>
            <br>
            <label for="op3" class="nuevaPregLabel">Opción 3</label>
            <input type="text" id="op3" class="nuevaPreg" required>
            <br>
            <label for="op4" class="nuevaPregLabel">Opción 4</label>
            <input type="text" id="op4" class="nuevaPreg" required>
            <br>
            <label for="respCorrecta">Respuesta correcta</label>
            <input type="number" id="respCorrecta" min="1" max="4" required>
            <input type="submit" value="Guardar" id="guardarPreg">
        </fieldset>
    </form>
</template>

<style scoped></style>
