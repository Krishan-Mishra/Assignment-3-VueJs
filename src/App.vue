<template>
  <the-header></the-header>
  <add-button></add-button>
  <stored-active-task-list :active-task="activeTask"></stored-active-task-list>
</template>

<script setup>
import { ref } from 'vue'
import TheHeader from './components/layouts/TheHeader.vue'
import AddButton from './components/layouts/AddButton.vue'
import StoredActiveTaskList from './components/activetasklist/StoredActiveTaskList.vue'
import Task_Data from '../dummy-data.js'

const activeTask = ref([])

activeTask.value = Task_Data
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
