<template>
  <div>
    <li class="todo-item" :class="{ 'todo-item--done': todo.complete }">
      <div class="todo-item__status">
        <i class="bi bi-check2"></i>
      </div>
      <span class="todo-item__text">Learn the basics of Vue</span>
      <button class="todo-item__remove-button">
        <i class="bi bi-trash3"></i>
      </button>
    </li>
  </div>
</template>

<script lang="ts">
import { defineComponent, type PropType } from 'vue'

export default defineComponent({
  props: {
    todo: {
      type: Object as PropType<{
        id: number
        text: String
        complete: boolean
      }>,
      required: true
    }
  }
})
</script>
