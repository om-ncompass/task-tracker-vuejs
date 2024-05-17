<template>
  <div 
    class="task" 
    :class="{ 'reminder': task.reminder }"
    @dblclick="handleReminderToggle(task.id)"
    >
    <h3>
      {{ task.text }}
      <i class="fas fa-times" @click="handleTaskDelete(task.id)"></i>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
export default {
  name: 'Task',
  props: {
    task: Object,
  },
  methods: {
    handleTaskDelete(taskId) {
      this.$emit('delete-task', taskId)
    },
    handleReminderToggle(taskId) {
      this.$emit('toggle-reminder', taskId)
    },
  }
}
</script>

<style scoped>
.fas {
  color: red;
}

.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}

.task.reminder {
  border-left: 5px solid green;
}

.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>