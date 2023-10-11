<template>
  <section>
    <base-button @click="toggleModal">Add Task</base-button>
    <add-task-modal v-if="showModal" @toggleModal="toggleModal"></add-task-modal>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import BaseButton from '../../UI/BaseButton.vue'
import AddTaskModal from '../AddTaskModal.vue'

const showModal = ref(false)

function toggleModal() {
  showModal.value = !showModal.value
}
</script>

<style scoped>
section {
  display: flex;
  justify-content: center;
  height: 4rem;
  align-items: center;
}
button {
  border-radius: 0.5rem;
}
</style>
