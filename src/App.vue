<template>
  <div>
    <h1>daily routine</h1>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        {{ task.name }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const tasks = ref([
  { name: 'kerjakan tugas pbk', completed: false },
  { name: 'olahraga', completed: false }
])
</script>
