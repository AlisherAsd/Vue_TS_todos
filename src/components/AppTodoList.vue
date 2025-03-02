<template>
    <ul class="todo-list">
        <AppTodoItem 
            v-for="todo in todos" 
            :todo="todo" 
            :key="todo.id"
            @toggle-todo="toggleTodo" 
            @delete-todo="deleteTodo"
        />
    </ul>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import AppTodoItem from './AppTodoItem.vue';
import { Todo } from '@/types/Todo';


export default defineComponent({
    components: {
        AppTodoItem,
    },
    props: {
        todos: {
            type: Array as PropType<Todo[]>
        }
    },
    methods: {
        toggleTodo(id: number) {
            this.$emit('toggleTodo', id)
        }, 
        deleteTodo(id: number) {
            this.$emit('deleteTodo', id)
        }
    },
    emits: {
        toggleTodo: (id: number) => id,
        deleteTodo: (id: number) => id
    }
})
</script>