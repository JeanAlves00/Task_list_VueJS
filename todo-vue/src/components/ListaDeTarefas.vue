<template>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(tarefa, index) in getTarefasFiltradas()" :key="index">
        <input @change="evento => tarefa.concluida = evento.target.checked" :checked="tarefa.concluida" type="checkbox">
        <label :class="{ done: tarefa.concluida }" class="ms-3" for="">
          {{ tarefa.descricao}}
        </label>
      </li>
    </ul>
</template>