<template>
  <div>
    <h2> Todos </h2>
    <router-link to='/'> Home </router-link>
    <hr>
    <AddTodo 
      @add-todo = 'addTodo'
    />
    <select v-model = 'filter'>
      <option value = 'all'>All</option>
      <option value = 'completed'>Completed</option>
      <option value = 'no-completed'>Not Completed</option>
    </select>
    <hr/>
    <Loader v-if = 'loading'/>
    <TodoList 
      v-else-if = 'filtresTodos.length'
      v-bind:todos = 'filtresTodos'
      @remove-todo = 'removeTodo'
    />
    <p v-else> No todos! </p>
  </div>
</template>

<script> 
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  components: {
    TodoList, AddTodo, Loader
  },
  // watch: {
  //   filter(value) {

  //   }
  // },
  computed: {
    filtresTodos() {
      if (this.filter === 'all') {
        return this.todos
      }

      if (this.filter === 'completed') {
        return this.todos.filter(t => t.completed)
      }

      if (this.filter === 'no-completed') {
        return this.todos.filter(t => !t.completed)
      }
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos')
      .then(response => response.json())
      .then(json => {
        this.todos = json
        this.loading = false
      })
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
      
      let todos = []
      this.todos.forEach((elem, index) => {
        elem.id = index + 1
        todos.push(elem)
      })
    },
    addTodo(title) {
      this.todos.push({ id: this.todos.length + 1, title, completed: false })
    }
  }
}
</script>