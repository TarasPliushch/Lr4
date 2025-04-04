// App.vue
<script>
export default {
  // ... інші властивості
  computed: {
    activeTodos() {
      return this.todos.filter(todo => !todo.completed)
    },
    completedTodos() {
      return this.todos.filter(todo => todo.completed)
    }
  }
}
</script>
