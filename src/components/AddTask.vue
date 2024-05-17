<template>
  <form
    class="add-form"
    :style="display ? { display: 'block' } : { display: 'none' }"
    @submit="handleSubmit"
  >
    <div class="form-control">
      <label>Task</label>
      <input type="text" v-model="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        type="text"
        v-model="day"
        name="day"
        placeholder="Add Day & Time"
      />
      <p>{{ day }}</p>
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input type="checkbox" name="reminder" v-model="reminder" />
    </div>

    <input type="submit" value="Save Task" class="btn btn-block"/>
  </form>
</template>

<script>
export default {
  name: "AddTask",
  data() {
    return {
      text: "",
      day: "",
      reminder: false,
    };
  },
  props: {
    display: Boolean,
  },
  methods: {
    handleSubmit(e) {
      e.preventDefault();
      if(!this.text) {
        alert('Please add a task.');
        return;
      } 
      this.$emit('handle-submit', { text: this.text, day: this.day, reminder: this.reminder });
      this.text = ''
      this.day = ''
      this.reminder = false
    }
  }
};
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
  cursor: pointer;
}
</style>