<script>
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue';
import AddTask from './components/AddTask.vue'
  export default{
    name: 'App',
    components: {
      Header,
      Tasks,
      AddTask
    },
    data() {
      return {
        tasks: [],
        showAddTask: false
      }
    },
    methods: {
      addTask(task) {
        this.tasks = [...this.tasks, task]
      },
      deleteTask(id) {
        if(confirm('Are you sure?')) {
          this.tasks = this.tasks.filter((task) => task.id !== id)
        }
      },
      toggleReminder(id) {
        this.tasks = this.tasks.map((task) => 
          task.id === id ? {...task, reminder: !task.reminder} : task
        )
      },
      toggleAddTask() {
        this.showAddTask = !this.showAddTask
      }
    },
    created() {
      this.tasks = [
        {
          id: 1,
          text: "Doctor Appointment",
          day: "March 1st at 2:30pm",
          reminder: true
        },
        {
          id: 2,
          text: "Dentist Appointment",
          day: "July 21st at 1:30pm",
          reminder: true
        },
        {
          id: 3,
          text: "Eye Appointment",
          day: "August 20th at 4:00pm",
          reminder: false
        }
      ]
    }
  }
</script>

<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" web_title="Task Tracker" :showAddTask="showAddTask"/>
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" /> 
    </div>
    <Tasks @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks" />
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
