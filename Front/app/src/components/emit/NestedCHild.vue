<template>
    <button @click="$emit('nested-data')">Nested data!</button>
</template>
<script setup>
defineEmits(['nested-data'])
</script>