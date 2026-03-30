<script setup lang="ts">
import Menu  from '@/components/tags/Menu.vue';
import Week1 from '@/components/week1/Week2ApiWrapperTask.vue'
import Week3 from '@/components/week3/Foundation.vue'
import Week4 from '@/components/week4/Foundation.vue'
import Week5 from '@/components/week5/Foundation.vue'
import Week2 from './components/week2/vModel.vue';
import Parent from '@/components/emit/Parent.vue';
</script>

<template>
  <div>
   <Menu/>
  </div>

  <div class="border-[10px] p-10 mt-[5vw] rounded-2xl border-blue-300 mb-[-50px] relative">
     <Parent/>
  </div>

  <div class="border-[10px] p-10 mt-[5vw] rounded-2xl border-blue-300 mb-[-50px] relative">
    <Week5/>
  </div>

  <div class="border-[10px] p-10 mt-[5vw] rounded-2xl border-blue-300 mb-5 relative">
    <Week4/>
  </div>

  <div class="border-[10px] p-10 rounded-2xl border-blue-300 mb-5 relative">
    <Week3/>
  </div>

  
  <div class="border-[10px] p-10 rounded-2xl border-blue-300 mb-[20px]">
    <Week2/>
  </div>

  <div class="border-[10px] p-10 rounded-2xl border-blue-300">
    <Week1/>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
