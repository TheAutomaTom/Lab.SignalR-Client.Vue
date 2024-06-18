<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()

const count = ref(0)

</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    
    <hr/> <!-- =========================== -->
    <h2>Input</h2>
    <h3>
      Username: <input/>      
    </h3>
    <h3 style="padding-bottom:2em;">
      Message: <input/>
    </h3>
    
    <hr/> <!-- =========================== -->
    <h2>Output</h2>
    <p>...</p>




  </div>

</template>

<style scoped>
</style>
