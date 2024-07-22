<template>
    <div class="task-list">
      <h2>Lista de Tarefas</h2>
      <ul>
        <li v-for="task in tasks" :key="task._id" class="task-item">
          <div class="task-details">
            <h3>{{ task.title }}</h3>
            <p>{{ task.description }}</p>
          </div>
          <button @click="completeTask(task._id)" class="complete-button">Concluir</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        tasks: []
      };
    },
    async created() {
      this.fetchTasks();
    },
    methods: {
      async fetchTasks() {
        try {
          const response = await axios.get('http://localhost:5000/api/tasks');
          this.tasks = response.data;
        } catch (error) {
          console.error('Erro ao buscar tarefas', error);
        }
      },
      async completeTask(taskId) {
        try {
          await axios.delete(`http://localhost:5000/api/tasks/${taskId}`);
          this.fetchTasks();
        } catch (error) {
          console.error('Erro ao concluir tarefa', error);
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .task-list {
    width: 100%;
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    background-color: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .task-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
    padding: 10px;
    background-color: #fff;
    border-radius: 4px;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  }
  
  .task-details {
    flex: 1;
  }
  
  .complete-button {
    background-color: #28a745;
    color: #fff;
    border: none;
    border-radius: 4px;
    padding: 5px 10px;
    cursor: pointer;
    font-size: 14px;
  }
  
  .complete-button:hover {
    background-color: #218838;
  }
  </style>
  
  