<template>
  <AddTask :display="display" @handle-submit="handleSubmit" />
  <Tasks
    @delete-task="handleDeleteTask"
    @toggle-reminder="handleReminderToggle"
    :tasks="tasks"
  />
</template> 

<script>
import AddTask from '../components/AddTask.vue'
import Tasks from '../components/Tasks.vue'

export default {
  name: 'Home',
  props: {
    display: Boolean
  },
  components: {
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
    }
  },
  methods: {
    async handleDeleteTask(taskId) {
      const response = await fetch(`http://localhost:5000/tasks/${taskId}`, {
        method: 'DELETE',
      });
      if(response.status == 200) {
        alert('Task deleted')
        this.tasks = this.tasks.filter(task => task.id !== taskId);
      } else {
        alert('Task not deleted.')
      }
    },
    async handleReminderToggle(taskId) {
      const taskToToggle = await this.fetchTask(taskId);
      const updatedTask = {...taskToToggle, reminder: !taskToToggle.reminder}
      await fetch(`http://localhost:5000/tasks/${taskId}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(updatedTask)
      });

      this.tasks = this.tasks.filter(task => {
        if(task.id === taskId) {
          task.reminder = !task.reminder
        }
        return task;
      })
    },
    async handleSubmit(task) {
      const response = await fetch('http://localhost:5000/tasks', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(task)
      })
      const data = await response.json()
      this.tasks = [...this.tasks, data];
    },
    async fetchTasks() {
      const response = fetch('http://localhost:5000/tasks')
      const data = (await response).json()
      return data;
    },
    async fetchTask(taskId) {
      const response = fetch(`http://localhost:5000/tasks/${taskId}`)
      const data = (await response).json()
      return data;
    }
  },
  async created() {
    // here, we make a fetch requets below when page first loads
    this.tasks = await this.fetchTasks()
  },
}
</script>