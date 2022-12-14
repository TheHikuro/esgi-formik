<script setup>
import { defineProps, defineEmits, defineExpose } from 'vue'
defineProps({
    initialValues: {
        type: Object,
        required: true
    },
    validator: {
        type: Function,
        required: true
    },
    onSubmit: {
        type: Function,
        required: true
    }
})
</script>

<template>
    <slot>

    </slot>

</template>

<style scoped>

</style>