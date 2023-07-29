<template>
    <footer class="app-footer">{{ amoutn }} more to do, {{ done }} done</footer>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    props: {
        amoutn: {
            type: Number,
            required: true
        },
        done: {
            type: Number,
            required: true
        },
    }
})
</script>