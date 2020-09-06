<template>
  <div>

    <router-link to="/">Home</router-link>

    <AddTodo 
      @add-todo="addTodo"
    />

    <Loader v-if="loading" />

    <TodoList
      v-else-if="todos.length"
      v-bind:todos="todos"
      @remove-todo="removeTodo"
    />

    <p v-else>Your todo list is empty!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList';
import AddTodo from '@/components/AddTodo';
import Loader from '@/components/Loader';

export default {
  name: 'App',
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=7')
      .then((response) => response.json())
      .then((json) => {
        setTimeout(() => {
          this.todos = json;
          this.loading = false;
        }, 1000)
      })
  },
  data: () => ({
    todos: [],
    loading: true,
  }),
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id != id)
    },
    addTodo(todo) {
      this.todos = [ ...this.todos, todo ];
    }
  },
  components: {
    AddTodo,
    TodoList,
    Loader
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
