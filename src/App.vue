<template>
  <div class="container">
    <Header 
    @toggle-add-task="toggleAddTask" 
    title="Task Tracker"
    :showAddTask="showAddTask"
    />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask"/>
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
  </div>
</template>



<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'

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
      showAddTask: false
    }
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id){
      // console.log('task', id);
      // alert popup before delete 
      if(confirm('Are you sure?')){
        // filter tasks array
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    toggleReminder(id){
      console.log(id);
      // map - manipulate the array, etc.
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: !task.reminder } : task)
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appointment',
        day: 'March 1st at 2:30pm',
        reminder: true,
      },
      {
        id: 2,
        text: 'Meeting at school',
        day: 'March 3rd at 2:30pm',
        reminder: true,
      },
      {
        id: 3,
        text: 'Student Appointment',
        day: 'March 5th at 10:30am',
        reminder: false,
      },
    ]
  }
}
</script>

<style>
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
  border-radius: 5pxs;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;

}
</style>
