<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive({
  tarefaTemp: 'aa',
  filtro: 'todas',
  tarefas: [
    {
      titulo: 'teste',
      finalizada: false,
    },
    {
      titulo: 'teste',
      finalizada: false,
    },
    {
      titulo: 'teste',
      finalizada: false,
    },
  ]
});

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
}
const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada === true)
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;
  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefasPendentes="getTarefasPendentes().length"></Cabecalho>
    <Formulario :trocarFiltro="evento => estado.filtro = evento.target.value" :tarefaTemp="estado.tarefaTemp" :editaTarefaTemp="evento => estado.tarefaTemp = evento.target.value" :cadastraTarefa="cadastraTarefa"></Formulario>
    <ListaDeTarefas :getTarefasFiltradas="getTarefasFiltradas()"></ListaDeTarefas>
  </div>
</template>
