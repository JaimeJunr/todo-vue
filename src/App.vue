<script setup>
import { reactive } from 'vue';
import CHeader from './components/Header.vue';
import CForm from './components/Form.vue';
import TaskList from './components/TaskList.vue';

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
    <CHeader :tarefas-pendestes="getTaskPendente()" />
    <CForm :editFiltro="ev => state.filtro = ev.target.value" :tempTask="state.tempTask" :editTempTask="ev => state.tempTask = ev.target.value" :taskCadastre="taskCadastre"/>
    <TaskList :getTaskFiltradas="getTaskFiltradas"/>
    
  </div>
</template>

