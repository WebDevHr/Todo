<template>
  <div id="app">
    <todoApp />
  </div>
</template>

<script>
import todoApp from './components/todoApp.vue'

export default {
  name: 'App',
  components: {
    todoApp
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
