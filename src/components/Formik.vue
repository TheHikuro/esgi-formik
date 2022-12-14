<script setup>
import { defineProps } from "vue";
defineProps({
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

const setFormValue = (name, value) => {
    value[name] = value;
};

const handleSubmit = () => {
    onSubmit({
        values,
    });
};

</script>

<template>
    <form @submit.prevent="handleSubmit">
        <slot :values="initialValues" :setFormValue="setFormValue" />
    </form>
</template>
  