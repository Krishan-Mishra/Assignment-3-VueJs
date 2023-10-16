<template>
  <li>
    <base-card>
      <header>
        <h1>{{ module }}</h1>
        <section>
          <font-awesome-icon :icon="faTrashCan" class="delete" @click="removeTask(id)" />
        </section>
      </header>
      <p>{{ content }}</p>
      <p>Duration: {{ duration }} days</p>
      <section class="checkbox">
        <input type="checkbox" @click="undoTaskCompleted(id)" />
        <label>UNDO The Task</label>
      </section>
    </base-card>
  </li>
</template>

<script setup>
import { inject, onMounted, ref } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faTrashCan, faPenToSquare } from '@fortawesome/free-solid-svg-icons'
import BaseCard from '../../UI/BaseCard.vue'

const addTaskfunc = inject('addTaskfunc')

const { completedTask, id, module, content, duration } = defineProps([
  'completedTask',
  'id',
  'module',
  'content',
  'duration'
])

const undoTaskCompleted = (id) => {
  const resIndex = completedTask.findIndex((res) => res.id === id)
  const activeTaskMoudle = completedTask[resIndex].module
  const activeTaskContent = completedTask[resIndex].content
  const activeTaskDuration = completedTask[resIndex].duration
  addTaskfunc(id, activeTaskMoudle, activeTaskContent, activeTaskDuration)
  setTimeout(() => {
    removeTask(id)
  }, 1200)
}

const removeTask = (id) => {
  const resIndex = completedTask.findIndex((res) => res.id === id)
  completedTask.splice(resIndex, 1)
  localStorage.setItem('completedtaskData', JSON.stringify(completedTask))
}
</script>

<style scoped>
li {
  margin: auto;
  max-width: 40rem;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
p {
  color: black;
  font-weight: bolder;
  margin: 0.5rem 0;
}
.delete,
.edit {
  color: #aa02f7;
  font-size: 1.5rem;
  padding: 0.4rem;
  cursor: pointer;
}
.delete:hover,
.edit:hover {
  color: #5d085d;
}

.checkbox {
  display: flex;
  justify-content: end;
}
.checkbox input {
  margin-right: 0.2rem;
}
</style>
