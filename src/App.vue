<template>
  <AppHeader />

  <AppFilters :activeFilter="activeFilter" @change-filter="changeFilter" />

  <main class="app-main">
    <AppTodoList :todoItem="filteredTodos" @toggleTodo="toggleTodo" @removeTodo="removeTodo" />
    <AppAddTodo @transfer-todo-text="transferTodoText" />
  </main>

  <AppFooter :filteredTodos="filteredTodos" />
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import AppFilters from './components/AppFilters.vue'
import AppHeader from './components/AppHeader.vue'
import AppTodoList from './components/AppTodoList.vue'
import AppAddTodo from './components/AppAddTodo.vue'
import AppFooter from './components/AppFooter.vue'
import type { Todo } from './types/todo'
import { filter } from './types/filter'

interface todotask {
  todos: Todo[]
  activeFilter: filter
}

export default defineComponent({
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter
  },
  data(): todotask {
    return {
      todos: [
        { id: 0, text: 'Learn the basics of Js', complete: true },
        { id: 1, text: 'Learn the basics of Vue', complete: true },
        { id: 2, text: 'Learn the basics of Typescript', complete: false }
      ],
      activeFilter: 'All'
    }
  },
  methods: {
    toggleTodo(id: number) {
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id)
      if (targetTodo) targetTodo.complete = !targetTodo.complete
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id)
    },
    transferTodoText(todo: Todo) {
      this.todos.push(todo)
    },
    changeFilter(filter: filter) {
      this.activeFilter = filter
    }
  },
  computed: {
    filteredTodos(): Todo[] {
      if (this.activeFilter === 'All') return this.todos
      else if (this.activeFilter === 'Active') {
        return this.todos.filter((todo: Todo) => !todo.complete)
      } else if (this.activeFilter === 'Done') {
        return this.todos.filter((todo: Todo) => todo.complete)
      }
      return this.todos
    }
  }
})
</script>
