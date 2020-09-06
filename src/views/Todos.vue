<template>
  <div>

    <router-link to="/">Home</router-link>

    <AddTodo 
      @add-todo="addTodo"
    />

    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
    </select>

    <hr />

    <Loader v-if="loading" />

    <TodoList
      v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
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
  // watch: {
  //   filter(value) {
  //     console.log(value);
  //   },
  // },
  computed: {
    filteredTodos() {
      if (this.filter === 'completed') {
        return this.todos.filter(({ completed}) => completed);
      } else if (this.filter === 'not-completed') {
        return this.todos.filter(({ completed}) => !completed);
      }

      return this.todos;
    },
  },
  data: () => ({
    todos: [],
    loading: true,
    filter: 'all',
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
