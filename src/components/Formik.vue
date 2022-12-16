<script setup>
import { defineProps, reactive, provide } from "vue";

const props = defineProps({
    initialValues: {
        type: Object,
        required: true,
    },
    validationSchema: {
        type: Object,
        required: true,
    },
    onSubmit: {
        type: Function,
        required: true,
    },
});

const values = reactive(props.initialValues);
provide("values", values);

const handleSubmit = (event) => {
    event.preventDefault();
    props.onSubmit(values);
};

</script>

<template>
    <form @submit.prevent="handleSubmit">
        <slot />
    </form>
</template>
  