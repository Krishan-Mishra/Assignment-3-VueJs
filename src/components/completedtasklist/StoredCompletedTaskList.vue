<template>
  <ul>
    <completed-task-list
      v-for="task in completedTask"
      :completedTask="completedTask"
      :key="task.id"
      :id="task.id"
      :module="task.module"
      :content="task.content"
      :duration="task.duration"
    ></completed-task-list>
  </ul>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import CompletedTaskList from './CompletedTaskList.vue'
const { completedTask } = defineProps(['completedTask'])
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
