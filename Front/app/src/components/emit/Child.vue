<template>
  <button @click="$emit('customEvent1',$event)">Event1 gone!</button>
   <NestedCHild @nested-data = "$emit('nested-data',$event)"/>
</template>
<script setup>
import NestedCHild from './NestedCHild.vue';
defineEmits(['customEvent1']) 
</script>
