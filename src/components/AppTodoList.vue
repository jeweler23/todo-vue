<template>
  <ul class="todo-list">
    <AppTodoItem
      v-for="todo in todoItem"
      :key="todo.id"
      :todo="{ id: todo.id, text: todo.text, complete: todo.complete }"
      @toggle-todo="toggleTodo"
      @removeTodo="removeTodo"
    />
  </ul>
</template>

<script lang="ts">
import { defineComponent, watch, type PropType } from 'vue'
import AppTodoItem from './AppTodoItem.vue'
import type { Todo } from '@/types/todo'

export default defineComponent({
  components: {
    AppTodoItem
  },
  props: {
    todoItem: {
      type: Array as PropType<Todo[]>
    }
  },
  methods: {
    toggleTodo(id: number) {
      this.$emit('toggleTodo', id)
    },
    removeTodo(id: number) {
      console.log(id)

      this.$emit('removeTodo', id)
    }
  },
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    removeTodo: (id: number) => Number.isInteger(id)
  }
})
</script>
