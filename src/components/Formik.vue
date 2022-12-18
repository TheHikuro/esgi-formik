<script setup>
import { defineProps, reactive, provide, toRefs } from "vue";

const props = defineProps({
    initialValues: {
        type: Object,
        required: true,
    },
    initialErrors: {
        type: Object,
        required: false,
        default: {},
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
const errors = reactive(props.initialErrors);

const onUpdatedValue = (id, value) => {
    values[id] = value;
};

provide("values", { values, onUpdatedValue });
provide("errors", { errors });


const handleSubmit = (event) => {
    event.preventDefault();
    Object.keys(errors).forEach((key) => {
        delete errors[key];
    });
    props.validationSchema
        .validate(values, { abortEarly: false })
        .then(() => {
            props.onSubmit(values);
        })
        .catch((err) => {
            err.inner.forEach((error) => {
                errors[error.path] = error.message;
            });
        });
};

</script>

<template>
    <form @submit.prevent="handleSubmit">
        <slot />
        <ul>
            <li v-for="(error, field) in errors" :key="field">{{ error }}</li>
        </ul>
    </form>
</template>
  