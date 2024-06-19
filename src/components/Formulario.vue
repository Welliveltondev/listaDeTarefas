<script setup>
    const props = defineProps(['cadastrarTarefa','tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>



<template>
    <form @submit.prevent="props.cadastrarTarefa()">
    <div class="row">
      <div class="col">
        <input :value="props.tarefaTemp" @change="props.editaTarefaTemp"  required type="text" class="form-control" placeholder="Inserir Nova tarefa">
      </div>
      <div class="col-md-2">
        <button type="submit" class=" btn btn-primary">Inserir</button>
      </div>
      <div class="col-md-2">
      <select @change="props.trocarFiltro" class="form-control">
        <option value="todas">Todas tarefas</option>
        <option value="todas">Pendentes</option>
        <option value="todas">Finalizadas</option>
      </select>
      </div>
    </div>
  </form>
</template>