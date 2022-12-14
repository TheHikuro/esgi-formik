<script>
import { defineProps } from "vue";
defineProps({
    name: {
        type: String,
        required: true,
    },
    label: {
        type: String,
        required: true,
    },
    placeholder: {
        type: String,
        required: false,
    },
    value: {
        type: Object,
        required: true,
    },
    type: {
        type: String,
        required: true,
    },
});
</script>
<template>
    <div>
        <label :for="name">{{ label }}</label>
        <input v-model="name" :id="name" :name="name" :value="value" @input="handleChange" :type="formtype"
            :placeholder="placeholder" />
    </div>
</template>