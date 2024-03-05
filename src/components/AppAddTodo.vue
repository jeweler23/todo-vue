<template>
  <section class="add-todo">
    <form class="add-todo__form" v-if="!isFormVisible" @submit.prevent="transferTodoText">
      <button class="close-button" type="button" @click="showForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input class="input" v-model="todoText" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
    <button v-else class="add-todo__show-form-button" @click="showForm">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<script lang="ts">
import type { Todo } from '@/types/todo'
import { defineComponent } from 'vue'

interface State {
  isFormVisible: boolean
  todoText: String
}

export default defineComponent({
  data(): State {
    return {
      isFormVisible: true,
      todoText: ''
    }
  },
  methods: {
    showForm() {
      this.isFormVisible = !this.isFormVisible
    },
    transferTodoText() {
      this.$emit('transferTodoText', {})
    }
  },
  emits: {
    transferTodoText: (todo: Todo) => todo
  }
})
</script>
