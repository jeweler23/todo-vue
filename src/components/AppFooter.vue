<template>
  <footer class="app-footer">{{ moreTasks }} more to do, {{ doneTasks }} done</footer>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import type { Todo } from '../types/todo'

export default defineComponent({
  props: {
    filteredTodos: {
      type: Object as PropType<Todo>
    }
  },
  computed: {
    moreTasks(): Number {
      return this.filteredTodos.reduce((acc: Number, item: Todo) => {
        if (!item.complete) {
          return (acc += 1)
        }
        return acc
      }, 0)
    },
    doneTasks(): Number {
      return this.filteredTodos.reduce((acc: Number, item: Todo) => {
        if (item.complete) {
          return (acc += 1)
        }
        return acc
      }, 0)
    }
  }
})
</script>
