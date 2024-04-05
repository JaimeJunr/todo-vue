<script setup>
    const props = defineProps(['taskCadastre', 'editTempTask', 'tempTask', 'editFiltro']);
</script>


<template>
    <form @submit.prevent="props.taskCadastre">
      <div class="row">
        <div class="col">
          <input @change="props.editTempTask" :value="props.tempTask"  required type="text" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="editFiltro" class="form-control">
            <option value="todas">Todas as Tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
</template>