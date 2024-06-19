<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false,
    },
    {
      titulo: 'Ir para academia',
      finalizada: true,
    }
  ]
})

const getTarefasPendente = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
  const {filtro} = estado;

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendente();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;

  }
}

const cadastrarTarefa = () => {
  const novaTarefa = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefas.push(novaTarefa);
  estado.tarefaTemp = '';
}
</script>

<template>
<div class="container">
  <header class="p-5 mb-4 mt-4 rounded-3">
    <h1>
      Minhas tarefas 
    </h1>
    <p>
      Você possui {{ getTarefasPendente().length }} tarefas pendentes
    </p>
  </header>
  <form @submit.prevent="cadastrarTarefa()">
    <div class="row">
      <div class="col">
        <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value"  required type="text" class="form-control" placeholder="Inserir Nova tarefa">
      </div>
      <div class="col-md-2">
        <button type="submit" class=" btn btn-primary">Inserir</button>
      </div>
      <div class="col-md-2">
      <select @change="evento => estado.filtro = evento.target.value" class="form-control">
        <option value="todas">Todas tarefas</option>
        <option value="todas">Pendentes</option>
        <option value="todas">Finalizadas</option>
      </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
      <input @change="evento  => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" type="checkbox" :id="tarefa.titulo">
      <label :class="{ done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
</div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
  border: 1px solid greenyellow;
}

</style>

