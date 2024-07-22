<template>
  <form @submit.prevent="addTask" class="add-task-form">
    <h2>Adicionar Tarefa</h2>
    <div>
      <label>Título</label>
      <input type="text" v-model="title" />
    </div>
    <div>
      <label>Descrição</label>
      <textarea v-model="description"></textarea>
    </div>
    <button type="submit">Adicionar</button>
  </form>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      title: '',
      description: ''
    };
  },
  methods: {
    async addTask() {
      try {
        await axios.post('http://localhost:5000/api/tasks', {
          title: this.title,
          description: this.description
        });
        this.title = '';
        this.description = '';
        this.$emit('taskAdded');
        alert('Tarefa adicionada com sucesso');
      } catch (error) {
        console.error('Erro ao adicionar tarefa', error);
      }
    }
  }
};
</script>

<style scoped>
.add-task-form {
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
}

.add-task-form h2 {
  margin-bottom: 10px;
}

.add-task-form div {
  margin-bottom: 10px;
}

.add-task-form label {
  display: block;
  margin-bottom: 5px;
}

.add-task-form input,
.add-task-form textarea {
  width: 100%;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.add-task-form button {
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  padding: 10px 15px;
  cursor: pointer;
}

.add-task-form button:hover {
  background-color: #0056b3;
}
</style>
