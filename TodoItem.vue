// components/TodoItem.vue
<template>
  <li class="todo-item" :class="{ completed: todo.completed }">
    <input
      type="checkbox"
      :checked="todo.completed"
      @change="$emit('toggle', todo.id)"
      class="todo-checkbox"
    />
    <span v-if="!isEditing" class="todo-text" @dblclick="startEditing">
      {{ todo.text }}
    </span>
    <input
      v-else
      type="text"
      v-model="editedText"
      @blur="finishEditing"
      @keyup.enter="finishEditing"
      @keyup.esc="cancelEditing"
      v-focus
      class="todo-edit-input"
    />
    <button @click="$emit('remove', todo.id)" class="todo-remove-btn">
      ×
    </button>
  </li>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      isEditing: false,
      editedText: this.todo.text
    }
  },
  methods: {
    startEditing() {
      this.isEditing = true
      this.editedText = this.todo.text
    },
    finishEditing() {
      if (this.editedText.trim()) {
        this.$emit('edit', { id: this.todo.id, text: this.editedText })
      }
      this.isEditing = false
    },
    cancelEditing() {
      this.isEditing = false
    }
  },
  directives: {
    focus: {
      inserted(el) {
        el.focus()
      }
    }
  }
}
</script>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  padding: 10px;
  margin: 5px 0;
  background: #f5f5f5;
  border-radius: 4px;
}
.todo-checkbox {
  margin-right: 10px;
}
.todo-text {
  flex: 1;
  cursor: pointer;
}
.todo-edit-input {
  flex: 1;
  padding: 5px;
  font-size: 16px;
}
.todo-remove-btn {
  background: none;
  border: none;
  color: #ff5252;
  font-size: 20px;
  cursor: pointer;
  margin-left: 10px;
}
.completed .todo-text {
  text-decoration: line-through;
  color: #888;
}
</style>
