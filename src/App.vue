<template>
  <div class="container">
    <h1>{{ title }}</h1>
    <Todo />
  </div>
</template>

<script>
import Todo from './components/todo.vue'
import './assets/global.css'

export default {
  name: 'App',
  data() {
    return {
      title: 'Todo List'
    }
  },
  components: { Todo }
}
</script>