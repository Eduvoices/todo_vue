<script setup>
const props = defineProps(['tarefas'])
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="evento => tarefa.completa = evento.target.checked" :checked="tarefa.completa"
                :id="tarefa.tarefa" type="checkbox">
            <label :class="{ done: tarefa.completa === true }" class="ms-3" :for="tarefa.tarefa">
                {{ tarefa.tarefa }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>
