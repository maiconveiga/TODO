<script setup>
import { reactive } from 'vue';


const estado = reactive({
  tarefaTemp: '',
  filtro: 'todas',
  tarefas:[
    {
      titulo: '',
      finalizada: false,
    },
    ] 
});

const getTarefasPendentes = () =>{
  return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
}
const getTarefasFinalizadas = () =>{
  return estado.tarefas.filter(tarefa => tarefa.finalizada === true)
}

const getTarefasFiltradas = () =>{
  const {filtro} = estado;
  switch(filtro){
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  } 
}

const cadastraTarefa = (e) =>{
  e.preventDefault();
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
}
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input @change="evento => estado.tarefaTemp = evento.target.value" required type="text" name="" id="" placeholder="Descrição da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" type="checkbox" :id="tarefa.titulo">
        <label :for="tarefa.titulo" class="ms-3" :class="{done:tarefa.finalizada === true}">
          {{tarefa.titulo}}
        </label>
      </li>
    </ul>
  </div>
  <form>

  </form>
</template>

<style scoped>

.done{
  text-decoration: line-through;
}
</style>
