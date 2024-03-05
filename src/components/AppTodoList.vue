<template>
  <ul class="todo-list">
    <AppTodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="{ id: todo.id, text: todo.text, complete: todo.complete }"
      @toggle-todo="toggleTodo"
      @remove-todo-item="removeTodo"
    />
  </ul>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import AppTodoItem from './AppTodoItem.vue'
import type { Todo } from '@/types/todo'

interface state {
  todos: Todo[]
}

export default defineComponent({
  components: {
    AppTodoItem
  },
  data(): state {
    return {
      todos: [
        { id: 0, text: 'Learn the basics of Js', complete: true },
        { id: 1, text: 'Learn the basics of Vue', complete: true },
        { id: 2, text: 'Learn the basics of Typescript', complete: false }
      ]
    }
  },
  methods: {
    toggleTodo(id: number) {
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id)
      if (targetTodo) targetTodo.complete = !targetTodo.complete
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id)
    }
  }
})
</script>
