<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button class="button" @click="setFilter('All')" :class="{'button--primary': activeFilter === 'All'}">All</button>
      <button class="button" @click="setFilter('Active')" :class="{'button--primary': activeFilter === 'Active'}">Active</button>
      <button class="button" @click="setFilter('Done')" :class="{'button--primary': activeFilter === 'Done'}">Done</button>
    </section>
  </aside>
</template>

<script lang="ts">
import { filter } from '@/types/Filter';
import { defineComponent, PropType } from 'vue';

export default defineComponent({
  props: {
    activeFilter: {
      type: String as PropType<filter>,
      required: true
    }
  },
  methods: {
    setFilter(filter: filter) {
      this.$emit('setFilter', filter)
    },
  },
  emits: {
    setFilter: (filter: filter) => filter
  }
})
</script>