<script>
export default {
    name: "Field",
    props: {
        as: { type: [Object, String], required: true },
        name: { type: String, required: true },
    },
};
</script>

<template>
    <component :is="as" :name="name">
        <slot />
    </component>
</template>