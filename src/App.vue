<template>
  <div id="app" class="app-container">
    <h1>Gerenciador de Tarefas</h1>
    <AddTask @taskAdded="fetchTasks" />
    <TaskList ref="taskList" />
  </div>
</template>

<script>
import AddTask from './components/AddTask.vue';
import TaskList from './components/TaskList.vue';

export default {
  name: 'App',
  components: {
    AddTask,
    TaskList,
  },
  methods: {
    fetchTasks() {
      this.$refs.taskList.fetchTasks();
    },
  },
};
</script>

<style>
.app-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
  background-color: #f0f0f0;
  min-height: 100vh;
}

h1 {
  margin-bottom: 20px;
}
</style>
