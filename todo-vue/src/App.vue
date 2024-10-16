<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';

  const estado = reactive({

    filtro:'todas',
    tarefaTemp: '',
    tarefas: [
      {
        descricao: 'Estudar ES6',
        concluida: false,
      },
      {
        descricao: 'Estudar TypeScript',
        concluida: true,
      },
      {
        descricao: 'Estudar Vue.js',
        concluida: false,
      }
    ],
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.concluida)
  }

  const getTarefasConcluidas = () => {
    return estado.tarefas.filter(tarefa => tarefa.concluida)
  }

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'concluidas':
        return getTarefasConcluidas();
      default:
        return estado.tarefas;
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      descricao: estado.tarefaTemp,
      concluida: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
  }

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario />
    <ListaDeTarefas />
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
