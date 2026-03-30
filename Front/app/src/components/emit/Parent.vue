<template>
<Child 
    @custom-event1="handleEvent"
    @nested-data = "handleEvent"
/>
</template>
<script setup>
import  Child from '@/components/emit/Child.vue'

function handleEvent(payload){
    console.log(payload)
}
</script>