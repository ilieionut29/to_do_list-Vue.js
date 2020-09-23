<template>
  <div id="app">
    <app-to-do ></app-to-do>
  </div>
</template>

<script>
import ToDoApp from './components/ToDoApp.vue'

export default {
  name: 'App',
  components: {
    appToDo: ToDoApp
  }
}
</script>

<style>

</style>
