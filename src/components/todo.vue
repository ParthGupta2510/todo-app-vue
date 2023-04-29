<template>
    <form v-on:submit.prevent="addTask">
      <input type="text" v-model="newTask">
      <button type="submit">Add Task</button>
    </form>
    <ul>
      <li v-for="(task, index) in tasks">
        <input type="checkbox" v-model="task.completed">
        <span v-bind:class="{ completed: task.completed }">{{ task.title }}</span>
        <input type="text" v-if="editingTask === task" v-model="task.title" v-on:blur="updateTask(task)" v-on:keyup.enter="updateTask(task)">
        <button v-on:click="editTask(task)">Edit</button>
        <button v-on:click="deleteTask(index)">Delete</button>
      </li>
    </ul>
</template>

<script>

export default {
  name: 'todo',
  data() {
    return {
        newTask: '',
        editingTask: {},
        tasks: JSON.parse(localStorage.getItem('tasks')) || []
      }
    },
methods: {
    addTask: function() {
        if (this.newTask.trim() === '') {
        return;
        }
        this.tasks.push({
        title: this.newTask,
        completed: false
        });
        this.newTask = '';
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    deleteTask: function(index) {
        this.tasks.splice(index, 1);
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    editTask: function(task) {
        this.editingTask = task;
    },
    updateTask: function(task) {
        this.editingTask = null;
        localStorage.setItem('tasks', JSON.stringify(this.tasks));  
    }
}}

</script>

<style>
    .completed {
      text-decoration: line-through;
    }
  </style>