<template>
  <div class="container">
    <h1>📝 Minha To-Do List</h1>

    <form @submit.prevent="addTask">
      <input
        v-model="newTask"
        placeholder="Digite uma tarefa"
      />
      <button type="submit">Adicionar</button>
    </form>

    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <span
          :class="{ done: task.done }"
          @click="toggleTask(index)"
        >
          {{ task.text }}
        </span>
        <button @click="removeTask(index)">❌</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const newTask = ref('')
const tasks = ref([])

function addTask() {
  if (newTask.value.trim() === '') return

  tasks.value.push({
    text: newTask.value,
    done: false
  })

  newTask.value = ''
}

function toggleTask(index) {
  tasks.value[index].done = !tasks.value[index].done
}

function removeTask(index) {
  tasks.value.splice(index, 1)
}
</script>

<style>
.container {
  max-width: 400px;
  margin: 40px auto;
  font-family: Arial, sans-serif;
}

input {
  padding: 8px;
  width: 70%;
}

button {
  margin-left: 8px;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}

.done {
  text-decoration: line-through;
  color: gray;
  cursor: pointer;
}

span {
  cursor: pointer;
}
</style>
