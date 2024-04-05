<script setup>
  const props = defineProps(['getTaskFiltradas'])
</script>


<template>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="task in getTaskFiltradas()">
        <input class="me-3" type="checkbox" @change="ev => task.finalizada = ev.target.checked" :id="task.titulo" :checked="task.finalizada" >
        <label :class="{ done: task.finalizada }" :for="task.titulo">
          {{ task.titulo }}
        </label>
      </li>
    </ul>
</template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
