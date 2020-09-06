<template>
  <div id="app">
    <h1>#TODO</h1>
    <TodoList
      v-bind:todos="todos"
      @remove-todo="removeTodo"
    />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList';

export default {
  name: 'App',
  data: () => ({
    todos: [
      {id: 1, title: 'Read some book', completed: false},
      {id: 2, title: 'Write some vue code', completed: false},
      {id: 3, title: 'Write some golang code', completed: false},
      {id: 4, title: 'Cook delicios meal', completed: false},
    ],
  }),
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id != id)
    },
  },
  components: {
    TodoList
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
