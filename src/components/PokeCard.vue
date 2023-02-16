<script setup>
import { computed} from 'vue'

const props = defineProps({
    name: {
        type: String,
        required: true
    },
    number: {
        type: Number,
        required: true
    }
})

// takes first letter of name and capitalizes it
const displayName = computed(() => {
    return props.name[0].toUpperCase() + props.name.substring(1)
})

</script>

<template>
    <li class="py-4 text-lg">{{ number }} - {{ displayName }}</li>
</template>

<style>
</style>
