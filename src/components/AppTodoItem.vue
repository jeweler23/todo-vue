<template>
  <div>
    <li class="todo-item" :class="{ 'todo-item--done': todo.complete }" @click="toggleTodo">
      <div class="todo-item__status">
        <i class="bi bi-check2"></i>
      </div>
      <span class="todo-item__text">{{ todo.text }}</span>
      <button class="todo-item__remove-button" @click.stop="removeTodoItem">
        <i class="bi bi-trash3"></i>
      </button>
    </li>
  </div>
</template>

<script lang="ts">
import { defineComponent, type PropType } from 'vue'
import type { Todo } from '@/types/todo'

export default defineComponent({
  props: {
    todo: {
      type: Object as PropType<Todo>,
      required: true
    }
  },
  methods: {
    toggleTodo() {
      this.$emit('toggleTodo', this.todo.id)
    },
    removeTodoItem() {
      this.$emit('removeTodoItem', this.todo.id)
    }
  },
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    removeTodoItem: (id: number) => Number.isInteger(id)
  }
})
</script>
