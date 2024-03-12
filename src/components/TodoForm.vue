<template>
    <div class="todo-form">
      <div class="input-container">
        <input type="text" v-model="task" placeholder="Enter task">
      </div>
      <div class="button-container">
        <button @click="addTodo">Add Task</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        task: ''
      };
    },
    methods: {
      addTodo() {
        if (this.task.trim() !== '') {
          this.$emit('add', {
            task: this.task,
            date: new Date().toLocaleString(),
            done: false
          });
          this.task = '';
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .todo-form {
    display: flex;
    margin-bottom: 20px;
  }
  
  .input-container {
    flex-grow: 1;
    margin-right: 10px; /* Add margin to the right */
  }
  
  .button-container {
    margin-left: 10px; /* Add margin to the left */
  }
  
  button {
    background-color: #4caf50;
    color: white;
    border: none;
    padding: 8px 12px;
    border-radius: 5px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #45a049;
  }
  </style>
  