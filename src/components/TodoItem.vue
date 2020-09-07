<template>
  <div>
    <li>
      <span :class="{done: todo.completed}">
        <input
          type="checkbox"
          v-on:change="todo.completed = !todo.completed"
        />
        <strong>{{ index }}</strong>
      {{ todo.title | capitalize }}
      </span>
      <button
        class="delete-btn"
        v-on:click="$emit('remove-todo', todo.id)"
      >
        &times;
      </button>
    </li>
  </div>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: Number
  },
  filters: {
    capitalize(value) {
      return `${value[0].toUpperCase()}${value.slice(1)}`
    }
  }
}
</script>

<style scoped>
  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
  }

  input {
    margin: 0 1rem;
  }

  .delete-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #ff0000;
    color: #ffffff;
    border-radius: 50%;
    font-weight: 800;
    font-size: 1.2rem;
    width: 2rem;
    height: 2rem;
    border: none;
    cursor: pointer;
  }

  .done {
    text-decoration: line-through;
  }
</style>