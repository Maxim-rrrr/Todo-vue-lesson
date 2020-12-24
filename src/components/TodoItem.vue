<template>
  <li>
    <span v-bind:class="{done: todo.completed}">
      <input type = "checkbox" v-on:change="todo.completed = !todo.completed">
      <string> {{ todo.id }} </string>
      {{ todo.title | uppercase }}
    </span>
    <button class = "rm" v-on:click = "$emit('remove-todo', todo.id)">&times;</button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  filters: {
    uppercase(value) {
      return value.toUpperCase()
    }
  }
}
</script>

<style scoped>
  li {
    border: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.5rem 2rem;
    margin-bottom: 1rem;
  }

  input {
    margin-right: 1rem;
  }

  .rm {
    background-color: red;
    color: #fff;
    border-radius: 50%;
    font-weight: bold;
    border: none;
  } 

  .done {
    text-decoration: line-through;
  }
</style>
