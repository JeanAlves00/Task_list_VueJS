<script setup>
  import { reactive } from 'vue';

  const estado = reactive({
    tarefas: [
      {
        id: 1,
        descricao: 'Estudar ES6',
        concluida: false,
      }
      {
        id: 2,
        descricao: 'Estudar TypeScript',
        concluida: true,
      }
      {
        id: 3,
        descricao: 'Estudar Vue.js',
        concluida: false,
      }
    ],
    filtroTarefas: 'todas',
    tarefaAdicionar: '',
  })

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui 7 tarefas pendentes
      </p>
    </header>
    <form>
      <div class="row">
        <div class="col">
          <input type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <section class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">pendentes</option>
            <option value="Finalizadas">Finalizadas</option>
          </section>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item">
        <input type="checkbox">
        <label class="ms-3" for="">
          estudar ES6
        </label>
      </li>
    </ul>
  </div>
  
  
</template>

<style scoped>

</style>
