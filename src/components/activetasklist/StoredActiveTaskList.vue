<template>
  <ul>
    <active-task-list
      v-for="task in activeTask"
      :key="task.id"
      :module="task.module"
      :content="task.content"
      :duration="task.duration"
    ></active-task-list>
  </ul>
</template>

<script setup>
import ActiveTaskList from './ActiveTaskList.vue'
const { activeTask } = defineProps(['activeTask'])
</script>

<style scoped>
ul {
  list-style: none;
  /* border: 2px solid yellow; */
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
