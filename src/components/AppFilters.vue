<template>
    <aside class="app-filters">
      <section class="toggle-group">
        <button 
          class="button" 
          v-for="filter in filters" :key="filter"
          :class="{'button--primary': ativeFilter === filter}" 
          @click="setFilter(filter)"
          >{{ filter }}</button>
      </section>
    </aside>
</template>

<script lang="ts">

import { Filter } from '@/types/Filter';
import { PropType, defineComponent } from 'vue'

interface State {
  filters: Filter[]
}


export default defineComponent({
  props: {
    ativeFilter: {
      type: String as PropType<Filter>,
      required: true,
    }
  },

  data(): State {
    return {
      filters: ['All', 'Active', 'Done']
    }
  },

  methods: {
    setFilter(filter: Filter) {
      this.$emit('setFilter', filter)
    }
  },

  emits: {
    setFilter: (filter: Filter) => filter
  }
})
</script>