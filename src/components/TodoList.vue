<template>
    <div class="todo-list">
        <div class="todo-header">
    <h2>To-Do List</h2>
       </div>
      <table v-if="todos.length > 0">
        <thead>
          <tr>
            <th>Task</th>
            <th>Date</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="todo in todos" :key="todo.id">
            <td>{{ todo.task }}</td>
            <td>{{ todo.date }}</td>
            <td>
              <button @click="markAsDone(todo)" v-if="!todo.done">Done</button>
              <span v-else>Completed</span>
            </td>
          </tr>
        </tbody>
      </table>
      <div v-else class="empty-message">No tasks available</div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['todos'],
    methods: {
      markAsDone(todo) {
        todo.done = true;
      }
    }
  };
  </script>
  
  <style>
  .todo-list {
    margin-top: 20px;
  }
  .todo-header {
  text-align: center; /* Center align the content */
}
  table {
    width: 100%;
    border-collapse: collapse;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }
  
  th, td {
    padding: 10px;
    border-bottom: 1px solid #ddd;
  }
  
  th {
    background-color: #f2f2f2;
    text-align: left;
  }
  
  button {
    background-color: #4caf50;
    color: white;
    border: none;
    padding: 5px 10px;
    border-radius: 3px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  button:hover {
    background-color: #45a049;
  }
  
  .empty-message {
    text-align: center;
    color: #808080;
    margin-top: 20px;
  }
  </style>
  