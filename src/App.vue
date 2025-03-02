<template>
  <AppHeader />
  <AppFilters :active-filter="activeFilter" @set-filter="setFilter" />
  <main class="app-main">
    <AppTodoList :todos="filtersTodo" @toggle-todo="toggleTodo" @delete-todo="deleteTodo" />
    <AppAddTodo @add-todo="addTodo" />
  </main>
  <AppFooter :stats="getStats" />
</template>


<script lang="ts">
import { defineComponent, DefineComponent } from 'vue';
import AppHeader from './components/AppHeader.vue';
import AppFilters from './components/AppFilters.vue';
import AppTodoList from './components/AppTodoList.vue';
import AppAddTodo from './components/AppAddTodo.vue';
import AppFooter from './components/AppFooter.vue';
import { Todo } from './types/Todo';
import { filter } from './types/Filter';
import { stats } from './types/Stats'; 

interface state {
  todos: Todo[],
  activeFilter: filter,
}

export default defineComponent({

  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter,
  },
  data(): state {
    return {
      todos: [
        { id: 1, text: 'asdasd', completed: true },
        { id: 2, text: 'bmpkpmkpmpkpmp', completed: false },
        { id: 3, text: 'asdce232', completed: false },
        { id: 4, text: 'dvppvopsdpasd', completed: false },
      ],
      activeFilter: 'All',
    }
  },
  methods: {
    addTodo(todo: Todo) {
      this.todos.push(todo);
    },
    toggleTodo(id: number) {
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id)
      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed;
      }
    },
    deleteTodo(id: number) {
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id)
    },
    setFilter(filter: filter) {
      this.activeFilter = filter
    },
  },
  computed: {
    filtersTodo(): Todo[] {
      if (this.activeFilter === 'All') {
        return this.todos
      }
      if (this.activeFilter === 'Active') {
        return this.activeTodos
      }
      if (this.activeFilter === 'Done') {
        return this.doneTodos
      }
      return this.todos
    },
    getStats(): stats {
      return {
        active: this.activeTodos.length,
        done: this.doneTodos.length
      }
    },
    activeTodos(): Todo[] {
      return this.todos.filter((todo: Todo) => !todo.completed)
    },
    doneTodos(): Todo[] {
      return this.todos.filter((todo: Todo) => todo.completed)
    }
  }
})

</script>