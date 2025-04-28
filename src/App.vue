<template>
  <div>
    <h1>daily routine</h1>
    <input v-model="newTask" placeholder="Tambah kegiatan baru" @keyup.enter="addTask" />
    <button @click="addTask">Tambah</button>
    <div>
      <label>
        <input type="checkbox" v-model="showOnlyActive" />
        Tampilkan yang belum selesai saja
      </label>
    </div>
    <ul>
      <li v-for="(task, index) in filteredTasks" :key="index">
        <input type="checkbox" v-model="task.completed" />
        <span :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">
  {{ task.name }}
</span>
        <button @click="deleteTask(index)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const tasks = ref([
  { name: 'kerjakan tugas pbk', completed: false },
  { name: 'olahraga', completed: false }
])
const newTask = ref('')
const showOnlyActive = ref(false)

function addTask() {
  if (newTask.value.trim() !== '') {
    tasks.value.push({ name: newTask.value, completed: false })
    newTask.value = ''
  }
}
function deleteTask(index) {
  tasks.value.splice(index, 1)
}

const filteredTasks = computed(() => {
  if (showOnlyActive.value) {
    return tasks.value.filter(task => !task.completed)
  }
  return tasks.value
})
const filteredTask = filteredTasks

</script>
