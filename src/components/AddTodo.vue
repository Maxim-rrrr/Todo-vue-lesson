<template>
  <form @submit.prevent = 'onSubmit'>
    <input type="text" v-model="title">
    <button type="submit"> Create </button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: ''
    }
  },
  methods: {
    onSubmit(event) {
      if (this.title.trim()) {
        this.$emit('add-todo', this.title)
        this.title = ''
      }
    }
  }
}
</script>

<style scoped>
  form {
    display: flex;
    justify-content: center;
  }

  input {
    width: 400px;
  }
</style>