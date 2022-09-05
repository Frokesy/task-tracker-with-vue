<template>
  <Header title="VTT" :showNewTask="showNewTask" @show-new-task="toggleNewTask" />
  <div v-if="showNewTask">
    <AddTask @add-task="addTask" />
  </div>
  <Tasks @toggle-task="toggleTask" @delete-task="deleteTask" :tasks="this.tasks" />
</template>

<script>
 import  Header  from './components/Header.vue'
import Tasks from './components/Tasks.vue';
import AddTask from './components/AddTask.vue';

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
},
  data() {
    return {
      tasks: [],
      showNewTask: false
    }
  },
  methods: {
    async addTask(task) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(task)
      })
      const data = await res.json()
      this.tasks = [data, ...this.tasks];
    },
    toggleNewTask() {
      this.showNewTask = !this.showNewTask;
    },
    async deleteTask(id) {
      if (confirm('Are you sure you want to delete this task?')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE'
        })
        res.status === 200 ? this.tasks = this.tasks.filter(task => task.id !== id) : alert('Error deleting task')
        this.tasks = this.tasks.filter(task => task.id !== id);
      }
    },
    async toggleTask(id) {
      const taskToToggle = await this.fetchTask(id);
      const updTask = {
        ...taskToToggle,
        reminder: !taskToToggle.reminder
      }
      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updTask)
      })
      const data = await res.json()
      
      this.tasks = this.tasks.map(task => task.id === id ? { ...task, reminder: data.reminder } : task);
    },
    async fetchTasks() {
      const res = await fetch('api/tasks');
      const data = await res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    }
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  margin: 40px auto;
  width: 85%;
  color: #000;
  padding: 10px 30px;
}
</style>
