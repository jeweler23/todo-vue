<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button
        v-for="filter in filters"
        :key="filter"
        class="button"
        :class="{ 'button--primary': activeFilter === filter }"
        @click="changeFilter(filter)"
      >
        {{ filter }}
      </button>
    </section>
  </aside>
</template>

<script lang="ts">
import { PropType, defineComponent } from 'vue'
import { filter } from '@/types/filter'

interface state {
  filters: filter[]
}

export default defineComponent({
  props: {
    activeFilter: {
      type: String as PropType<filter>,
      required: true
    }
  },
  data(): state {
    return {
      filters: ['All', 'Active', 'Done']
    }
  },
  methods: {
    changeFilter(filter: filter) {
      this.$emit('changeFilter', filter)
    }
  },
  emits: {
    changeFilter: (filter: filter) => filter
  }
})
</script>
