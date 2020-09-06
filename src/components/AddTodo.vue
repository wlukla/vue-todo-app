<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title" />
    <button>Add</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: '',
    }
  },
  methods: {
    onSubmit() {
      if (this.title) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          completed: false,
        };

        this.$emit('add-todo', newTodo);
        this.title = "";
      }
    }
  }
}
</script>

<style scoped>
  form {
    display: flex;
    justify-content: center;
    margin-bottom: 2rem;
  }

  input {
    width: 80%;
    min-width: 100px;
    max-width: 400px;
    margin-right: .5rem;
  }
</style>