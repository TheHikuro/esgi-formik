<script setup>
import { inject } from 'vue';

const props = defineProps({
    as: {
        type: [Object, String],
        required: true,
    },
    name: {
        type: String,
        required: true,
    },
});

const {values, onUpdatedValue} = inject('values');
</script>
<template>
    <component :is="as" :name="name" :value="values[name]" @input="onUpdatedValue(name, $event.target.value)">
        <slot />
    </component>
</template>

<style scoped>
input {
    padding: 0.5rem;
    border: none;
    border-radius: 0.25rem;
    background-color: rgb(65, 65, 65);
    color: rgb(255, 255, 255);
    font-weight: bold;
}

select {
    padding: 0.5rem;
    border: none;
    border-radius: 0.25rem;
    background-color: rgb(65, 65, 65);
    color: rgb(255, 255, 255);
    font-weight: bold;
}

textarea {
    padding: 0.5rem;
    border: none;
    border-radius: 0.25rem;
    background-color: rgb(65, 65, 65);
    color: rgb(255, 255, 255);
    font-weight: bold;
}
</style>