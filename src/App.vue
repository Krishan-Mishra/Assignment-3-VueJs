<template>
  <the-header></the-header>
  <base-card>
    <base-button @click="setSelectedTab('stored-active-task')">Active Task</base-button>
    <base-button @click="setSelectedTab('stored-completed-task')">Completed Task</base-button>
  </base-card>
  <add-button v-if="selectedTab === 'stored-active-task'"></add-button>
  <stored-active-task-list
    :activeTask="activeTask"
    v-if="selectedTab === 'stored-active-task'"
  ></stored-active-task-list>
  <stored-completed-task-list :completedTask="completedTask" v-else></stored-completed-task-list>
</template>

<script setup>
import { ref, provide, onMounted } from 'vue'
import TheHeader from './components/layouts/TheHeader.vue'
import AddButton from './components/layouts/AddButton.vue'
import StoredActiveTaskList from './components/activetasklist/StoredActiveTaskList.vue'
import StoredCompletedTaskList from './components/completedtasklist/StoredCompletedTaskList.vue'
import BaseCard from './UI/BaseCard.vue'
import BaseButton from './UI/BaseButton.vue'

onMounted(() => {
  const storeTask = localStorage.getItem('taskData')
  if (storeTask) {
    activeTask.value = JSON.parse(storeTask)
  }
})

onMounted(() => {
  const storeTask = localStorage.getItem('completedtaskData')
  if (storeTask) {
    completedTask.value = JSON.parse(storeTask)
  }
})

const selectedTab = ref('stored-active-task')
const setSelectedTab = (tab) => {
  selectedTab.value = tab
}

const activeTask = ref([])
const completedTask = ref([])

const addTaskfunc = (id, module, content, duration) => {
  activeTask.value.unshift({ id, module, content, duration })
  localStorage.setItem('taskData', JSON.stringify(activeTask.value))
}

const addCompletedTaskFunc = (id, module, content, duration) => {
  completedTask.value.push({ id, module, content, duration })
  localStorage.setItem('completedtaskData', JSON.stringify(completedTask.value))
}

provide('addTaskfunc', addTaskfunc)
provide('addCompletedTaskFunc', addCompletedTaskFunc)
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

<style scoped>
div {
  display: flex;
  justify-content: center;
  margin: 0 auto;
  margin-top: 1rem;
  width: 20rem;
  
}
button {
  margin-right: 0.4rem;
  border-radius: 0.5rem;
}
</style>
