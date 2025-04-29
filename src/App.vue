<template>
  <div>
    <h1>⛅daily routine⛅</h1>
    <hr class="divider" />
    <input type="text" v-model="newTask" placeholder="Tambah kegiatan baru" @keyup.enter="addTask" />
    <button @click="addTask">Tambah</button>
    <div class="input-container">
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
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css">
  <button @click="deleteTask(index)">
  <i class="fas fa-trash-alt"></i>
</button>
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
<style scoped>
div {
  max-width: 600px;
  margin: 20px auto;
  padding: 20px;
  background-color: #dff0f3;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

h1 {
  text-align: center;
  color: #2B5288;
  margin-bottom: 20px;
  font-family: 'Pacifico', cursive;
  font-size: 32px;
  text-transform: capitalize;
}
.divider {
  border: none;
  height: 2px;
  background: linear-gradient(to right, #2B5288, #E5E0D9);
  margin: 10px 0 20px;
  border-radius: 5px;
}

input[type="text"] {
  width: 60%; 
  padding: 8px 12px; 
  font-size: 15px;  
  margin-right: 10px;
  border: 2px solid #2B5288;
  border-radius: 10px;
  outline: none;
  background-color: #ffffff;
  color: #2B5288;
  box-shadow: 0 2px 6px rgba(107, 33, 59, 0.3);
  transition: all 0.3s ease;
}

input[type="text"]::placeholder {
  color: #abb7c8;
  font-style: italic;
}

input[type="text"]:focus {
  border-color: #2B5288;
  box-shadow: 0 0 8px rgba(72, 60, 127, 0.4);
  background-color: #fff8fb;
}

button {
  padding: 8px 15px;
  font-family: 'Pacifico', cursive;
  font-size: 15px;
  background-color: #87CEFA;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #71abd0;
}


label {
  display: flex;
  align-items: center;
  margin: 20px 5;
  font-size: 15px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #ffffff;
  padding: 15px 16px;
  margin-bottom: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
}

li span {
  flex: 1;
  margin-left: 12px;
  font-size: 16px;
  color: #333;
}

li input[type="checkbox"] {
  transform: scale(1.2);
}

li button {
  background-color: #87CEFA;
  padding: 6px 10px;
  font-size: 14px;
  border-radius: 6px;
}

li button:hover {
  background-color: #87CEFA;
}
</style>

