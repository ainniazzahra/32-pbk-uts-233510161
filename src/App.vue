<template>
  <div>
    <h1>daily routine</h1>
    <input v-model="newTask" placeholder="Tambah kegiatan baru" @keyup.enter="addTask" />
    <button @click="addTask">Tambah</button>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <input type="checkbox" v-model="task.completed" />
        <span>{{ task.name }}</span>
        <button @click="deleteTask(index)">Hapus</button>
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
const newTask = ref('')

function addTask() {
  if (newTask.value.trim() !== '') {
    tasks.value.push({ name: newTask.value, completed: false })
    newTask.value = ''
  }
}
function deleteTask(index) {
  tasks.value.splice(index, 1)
}

</script>
