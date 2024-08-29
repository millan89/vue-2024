<!-- COMPOSITION API -->

<script setup>
import {ref, onMounted} from 'vue';

const name = ref('John dor');
const status = ref('active');
const tasks = ref(['Task one', 'Task two', 'Task three']);
const newTask = ref('');

const toggleStatus = () => {
  if(status.value === 'active'){
    status.value = 'pending'
  } else if(status.value === 'pending'){
    status.value = 'inactive';
  } else {
    status.value = 'active';
  }
}

const addTask = () => {
  if(newTask.value.trim() !== ""){
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
}

const deleteTask = (index)=>{
  tasks.value.splice(index, 1);
}

onMounted(async () => {
  try {
    const response = await fetch('http://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    tasks.value = data.map((task)=> task.title)
  } catch (error) {
    console.log('Error fetching tasks')
  }
});
</script>

<template>
  <h1>{{name}}</h1>  
  <p v-if="status === 'active'">User is astive</p>
  <p v-else-if="status === 'pending'">User pending</p>
  <p v-else>User is inactive</p>

<form @submit.prevent="addTask">
  <label for="newTask">Add task</label>
  <input type="text" id="newTask" name="newTask" v-model="newTask">
  <button type="submit">Add task</button>
</form>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      {{ task }}
      <button @click="deleteTask(index)">X</button>
    </li>
  </ul>
<br>
<br>
  <button @click="toggleStatus">Change status</button>
</template>
