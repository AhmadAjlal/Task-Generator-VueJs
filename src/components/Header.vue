<template>
  <header>
    <h1>{{ title }}</h1>
    <Button v-show="homePage" :btn-name="showAddTask ? 'Close' : 'Add Task'" :color="showAddTask ? 'red' : 'green'"
            @btn-click="$emit('toggle-add-task')"/>
  </header>
</template>

<script>
import Button from "@/components/Button.vue";

export default {
  name: "HeaderComponent",
  props: {
    title: String,
    showAddTask: Boolean,
  },
  components: {
    Button,
  },
  computed: {
    homePage() {
      if (this.$route.path === '/') {
        return true;
      } else {
        return false;
      }
    }
  },
}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>