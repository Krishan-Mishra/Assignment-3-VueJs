<template>
  <the-header></the-header>
  <add-button></add-button>
  <stored-active-task-list :activeTask="activeTask"></stored-active-task-list>
</template>

<script setup>
import { ref, provide, onMounted } from 'vue'
import TheHeader from './components/layouts/TheHeader.vue'
import AddButton from './components/layouts/AddButton.vue'
import StoredActiveTaskList from './components/activetasklist/StoredActiveTaskList.vue'

onMounted(() => {
  const storeTask = localStorage.getItem('taskData')
  if (storeTask) {
    activeTask.value = JSON.parse(storeTask)
  }
})

const activeTask = ref([])

const addTaskfunc = (id, module, content, duration) => {
  activeTask.value.unshift({ id, module, content, duration })
  localStorage.setItem('taskData', JSON.stringify(activeTask.value))
}

provide('addTaskfunc', addTaskfunc)
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Roboto', sans-serif;
  margin: 0;
}
</style>
