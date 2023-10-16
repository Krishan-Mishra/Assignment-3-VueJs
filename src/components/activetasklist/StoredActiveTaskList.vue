<template>
  <ul>
    <active-task-list
      v-for="task in activeTask"
      :activeTask="activeTask"
      :key="task.id"
      :id="task.id"
      :module="task.module"
      :content="task.content"
      :duration="task.duration"
    ></active-task-list>
  </ul>
</template>

<script setup>
import { ref } from 'vue'
import ActiveTaskList from './ActiveTaskList.vue'
const { activeTask } = defineProps(['activeTask'])
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>