<script setup lang="ts">
import { reactive } from 'vue';

  const state = reactive({
    filtro: "todas",
    tempTask: '',
    tarefas: [
      {
        titulo:"Estudar ES6",
        finalizada: false
      },
      {
        titulo:"Estudar SASS",
        finalizada: true
      },
      {
        titulo:"Estudar React",
        finalizada: true
      }
    ]
  })

  const getTaskPendente = () => {
    return state.tarefas.filter(task => !task.finalizada)
  }
  const getTaskFinalizadas = () => {
    return state.tarefas.filter(task => task.finalizada)
  }

  const getTaskFiltradas = () => {
    const filtro = state.filtro
    
    switch (filtro){
      case "pendentes":
        return getTaskPendente()

      case "finalizadas":
        return getTaskFinalizadas()

      default:
        return state.tarefas
    }
  }

  const taskCadastre = () => {
    const task = {
      titulo: state.tempTask,
      finalizada: false
    }
    state.tarefas.push(task);
    state.tempTask = '';
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTaskPendente().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="taskCadastre">
      <div class="row">
        <div class="col">
          <input :value="state.tempTask" @change="ev => state.tempTask = ev.target.value" required type="text" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="ev => state.filtro = ev.target.value" class="form-control">
            <option value="todas">Todas as Tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="task in getTaskFiltradas()">
        <input class="me-3" type="checkbox" @change="ev => task.finalizada = ev.target.checked" :id="task.titulo" :checked="task.finalizada" >
        <label :class="{ done: task.finalizada }" :for="task.titulo">
          {{ task.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
