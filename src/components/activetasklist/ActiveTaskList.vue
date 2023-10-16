<template>
  <li>
    <base-card>
      <header>
        <h1>{{ currentModule }}</h1>
        <section>
          <font-awesome-icon :icon="faTrashCan" class="delete" @click="removeTask(id)" />
          <font-awesome-icon :icon="faPenToSquare" class="edit" @click="toggleModal" />
        </section>
      </header>
      <p>{{ currentContent }}</p>
      <p>Duration: {{ currentDuration }} days</p>
      <section class="checkbox">
        <input type="checkbox" :value="id" :id="id" @click="taskCompleted(id)" />
        <label :for="id">Mark This Task Done </label>
      </section>
    </base-card>
  </li>
  <edit-task-modal
    v-if="showModal"
    @toggleModal="toggleModal"
    @updateTaskValue="updateTaskValue"
    :module.sync="module"
    :content.sync="content"
    :duration.sync="duration"
  ></edit-task-modal>
</template>

<script setup>
import { inject, ref } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faTrashCan, faPenToSquare } from '@fortawesome/free-solid-svg-icons'
import EditTaskModal from '../modal/EditTaskModal.vue'
const { activeTask, module, content, duration } = defineProps([
  'activeTask',
  'id',
  'module',
  'content',
  'duration'
])

const emit = defineEmits(['taskCompleted'])
const addCompletedTaskFunc = inject('addCompletedTaskFunc')

const currentModule = ref(module)
const currentContent = ref(content)
const currentDuration = ref(duration)

const showModal = ref(false)

const removeTask = (id) => {
  const resIndex = activeTask.findIndex((res) => res.id === id)
  activeTask.splice(resIndex, 1)
  localStorage.setItem('taskData', JSON.stringify(activeTask))
}

const updateTaskValue = (updatedValue) => {
  const resIndex = activeTask.findIndex((res) => res.id === currentModule.value)
  currentModule.value = updatedValue.localModule.value
  currentContent.value = updatedValue.localContent.value
  currentDuration.value = updatedValue.localDuration.value
  activeTask[resIndex].id = currentModule.value
  activeTask[resIndex].module = currentModule.value
  activeTask[resIndex].content = currentContent.value
  activeTask[resIndex].duration = currentDuration.value
  localStorage.setItem('taskData', JSON.stringify(activeTask))
}

const toggleModal = () => {
  showModal.value = !showModal.value
}

const taskCompleted = (id) => {
  const resIndex = activeTask.findIndex((res) => res.id === id)
  const completedTaskMoudle = activeTask[resIndex].module
  const completedTaskContent = activeTask[resIndex].content
  const completedTaskDuration = activeTask[resIndex].duration
  addCompletedTaskFunc(id, completedTaskMoudle, completedTaskContent, completedTaskDuration)
  setTimeout(() => {
    removeTask(id)
  }, 1200)
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
