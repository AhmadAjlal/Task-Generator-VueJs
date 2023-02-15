<template>
  <AddTask v-if="showAddTask" @add-task="addTask"/>
  <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>


</template>

<script>
import Tasks from "@/components/Tasks.vue";
import AddTask from "@/components/AddTask.vue";

export default {
  name: "HomeComponent",
  props: {
    showAddTask: Boolean,
  },
  components: {
    Tasks,
    AddTask,
  },

  data() {
    return {
      tasks: [],
    }
  },

  methods: {

    async addTask(task) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task),
      });
      const data = await res.json();

      this.tasks = [...this.tasks, data];
    },

    async deleteTask(id) {
      if (confirm('Are you sure you want to delete this Task?')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',
        })
        res.status === 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert("Error Deleting Task");
      }
    },

    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id);
      const updateTask = {...taskToToggle, remainder: !taskToToggle.remainder};
      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updateTask),
      });
      const data = await res.json();
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, remainder: data.remainder} : task);
    },

    async fetchTasks() {
      const res = await fetch('api/tasks');
      const myData = await res.json();

      return myData;
    },

    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const myData = await res.json();
      return myData;
    }
  },

  async created() {
    this.tasks = await this.fetchTasks();
  }
}
</script>

<style scoped>

</style>