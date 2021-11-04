<template>
  <div id="app"
       style="background-color: #E7D2CC; height: 100vh; position: fixed; width: 100vw"
  >
    <todo-app></todo-app>
  </div>
</template>

<script>
import TodoApp from './components/TodoApp.vue'

export default {
  name: 'App',
  components: {
    TodoApp
  }
}
</script>


