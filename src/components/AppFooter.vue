<template>
    <footer class="app-footer">{{ stats.active }} more to do, {{ stats.done  }} done</footer>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';

interface stats {
    active: number,
    done: number
}

export default defineComponent({
    props: {
        stats: {
            type: Object as PropType<stats>,
            required: true
        }
    }
})
</script>