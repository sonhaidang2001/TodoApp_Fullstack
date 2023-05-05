<template>
  <div id="todo-app">
    <Header />
    <Todo />
  </div>
</template>

<script>
import Header from '../src/components/Header.vue'
import Todo from '../src/components/Todo.vue'

export default {
  name: 'App',
  components: { Header, Todo }
}
</script>

<style>
</style>