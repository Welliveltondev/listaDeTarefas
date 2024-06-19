<script setup>
const props = defineProps(['tarefas'])
</script>


<template>
    <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in props.tarefas"></li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
    border: 1px solid greenyellow;
}
</style>

