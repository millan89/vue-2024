<!-- OPTIONS -->

<script>
  export default {
    data(){
      return {
        name: "John dor",
        status: 'dfdf',
        tasks: ['Task one', 'Task two', 'Task three'],
        link: "http://www.google.com",
      }
    },
    methods: {
      toggleStatus() {
        if(this.status === 'active'){
          this.status = 'pending'
        } else if(this.status === 'pending'){
          this.status = 'inactive';
        } else {
          this.status = 'active';
        }
      }
    }
  }
</script>

<template>
  <h1>{{name}}</h1>  
  <p v-if="status === 'active'">User is astive</p>
  <p v-else-if="status === 'pending'">User pending</p>
  <p v-else>User is inactive</p>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <!-- <a v-bind:href="link">Go to goodle</a> -->
  <a :href="link">Go to goodle</a>
<br>
<br>
  <button @click="toggleStatus">Change status</button>
</template>
