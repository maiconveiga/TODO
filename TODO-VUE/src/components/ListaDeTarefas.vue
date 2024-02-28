<script setup>
const props = defineProps(['getTarefasFiltradas']);
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.getTarefasFiltradas">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                type="checkbox" :id="tarefa.titulo">
            <label :for="tarefa.titulo" class="ms-3" :class="{ done: tarefa.finalizada === true }">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>