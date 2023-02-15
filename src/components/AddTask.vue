<template>
  <form class="add-form" @submit="onSubmit">
    <div class="form-control">
      <label>Task</label>
      <input v-model="text" name="text" placeholder="Add Task Name" type="text">
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input v-model="day" name="day" placeholder="Add Day & Time" type="text">
    </div>
    <div class="form-control form-control-check">
      <label>Set Remainder</label>
      <input v-model="remainder" name="remainder" type="checkbox">
    </div>
    <input class="btn btn-block" type="submit" value="Save Task">
  </form>

</template>

<script>
export default {
  name: "AddTask",
  data() {
    return {
      text: '',
      day: '',
      remainder: false
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();

      if (!this.text) {
        alert('Please add task Name');
        return
      }
      const newTask = {
        text: this.text,
        day: this.day,
        remainder: this.remainder
      }

      this.$emit('add-task', newTask);

      this.text = '';
      this.day = '';
      this.remainder = false;
    }
  }
}
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
}

</style>