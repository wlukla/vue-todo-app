<template>
  <div>

    <router-link to="/">Home</router-link>

    <AddTodo 
      @add-todo="addTodo"
    />
    <TodoList
      v-if="todos.length"
      v-bind:todos="todos"
      @remove-todo="removeTodo"
    />

    <p v-else>Your todo list is empty!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList';
import AddTodo from '@/components/AddTodo';

export default {
  name: 'App',
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=7')
      .then((response) => response.json())
      .then((json) => {
        this.todos = json;
      })
  },
  data: () => ({
    todos: [],
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
