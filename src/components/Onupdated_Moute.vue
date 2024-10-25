<script setup>
import { ref, onUpdated, onMounted, onBeforeMount, onBeforeUpdate } from 'vue'

const count = ref(0)



onBeforeMount(()=>{
  console.log("Before Mouted Run!");
  onUpdated(()=>{
    console.log("test");
  });
  
});
onMounted(()=>{
  console.log("run onmouted stage !");
  count.value = 10;
});


onBeforeUpdate(()=>{
  console.log("onBeforeUpdate !!");
  
});
onUpdated(() => {
  // text content should be the same as current `count.value`
  console.log(document.getElementById('count').textContent)
})
</script>

<template>
  <button class="btn btn-sm btn-outline-primary" id="count" @click="count++">{{ count }}</button>
</template>