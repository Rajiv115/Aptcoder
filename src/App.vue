<template>
  <div id="app">
    <Navbar />
    <div class="container">
      <div class="todo-form">
        <input type="text" v-model="task" placeholder="Enter task">
        <button @click="addTodo" :class="{ 'active': task.trim() !== '' }">Add Task</button>
      </div>
      <TodoList :todos="todos" />
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue';
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: {
    Navbar,
    TodoList
  },
  data() {
    return {
      task: '',
      todos: []
    };
  },
  methods: {
    async fetchTodos() {
      try {
        const response = await fetch('http://localhost:3000/todos');
        this.todos = await response.json();
      } catch (error) {
        console.error('Error fetching todos:', error);
      }
    },
    async addTodo() {
      if (this.task.trim() !== '') {
        try {
          const response = await fetch('http://localhost:3000/todos', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify({
              task: this.task,
              date: new Date().toLocaleString(),
              done: false
            })
          });
          const newTodo = await response.json();
          this.todos.push(newTodo);
          this.task = '';
        } catch (error) {
          console.error('Error adding todo:', error);
        }
      }
    }
  },
  created() {
    this.fetchTodos();
  }
};
</script>

<style>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.todo-form {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

input[type="text"] {
  flex-grow: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px 0 0 5px;
  font-size: 1em;
}

button {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 0 5px 5px 0;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #45a049;
}

.active {
  background-color: #45a049;
}
</style>
