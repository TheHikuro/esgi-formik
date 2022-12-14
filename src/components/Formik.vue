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

const formValues = reactive(props.initialValues);
provide("formValues", formValues);

const handleChangeValue = (name, value) => {
    formValues[name] = value;
};

const handleSubmit = () => {
    console.log(formValues);
    props.onSubmit(formValues);
};

</script>

<template>
    <form @submit.prevent="handleSubmit">
        <slot :value="formValues" :set-value="handleChangeValue" />
    </form>
</template>
  