<script setup>
  import { reactive } from 'vue';

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

  const getTarefasPendente = () => {
    return estado.tarefas.filter(tarefa => !tarefa.concluida)
  }

  const getTarefasConcluidas = () => {
    return estado.tarefas.filter(tarefa => tarefa.concluida)
  }

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendente();
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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasPendente().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
            <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">pendentes</option>
            <option value="concluidas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(tarefa, index) in getTarefasFiltradas()" :key="index">
        <input @change="evento => tarefa.concluida = evento.target.checked" :checked="tarefa.concluida" type="checkbox">
        <label :class="{ done: tarefa.concluida }" class="ms-3" for="">
          {{ tarefa.descricao}}
        </label>
      </li>
    </ul>
  </div>
  
  
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
a