<template>
  <div class="modal" @click="toggleModal">
    <div class="modal-content" @click.stop>
      <h2>Add Task</h2>
      <form @submit.prevent="handleSubmit">
        <div class="form-group">
          <label for="module">Module:</label>
          <input type="text" id="module" v-model="module" required />
        </div>
        <div class="form-group">
          <label for="content">Content:</label>
          <textarea id="content" v-model="content" rows="4" required></textarea>
        </div>
        <div class="form-group">
          <label for="duration">Duration (in days):</label>
          <input type="number" id="duration" v-model="duration" required />
        </div>
        <div class="form-group">
          <button type="submit">Submit</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref, provide } from 'vue'

const emit = defineEmits(['toggleModal'])
const module = ref(null)
const content = ref(null)
const duration = ref(0)

const handleSubmit = () => {
  console.log('hello')
}

const toggleModal = () => {
  emit('toggleModal')
}
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: white;
  padding: 1.28rem;
  border-radius: 0.4rem;
  width: 25rem;
}

.form-group {
  margin-bottom: 1.25rem;
  margin-top: 0.5rem;
}

label {
  display: block;
  font-weight: bold;
}

input[type='text'],
input[type='number'],
textarea {
  width: 100%;
  padding: 0.63rem;
  border: 1px solid #ccc;
  border-radius: 0.32rem;
  font-size: 1rem;
}

button {
  background-color: #aa02f7;
  color: white;
  border: none;
  padding: 0.625rem 1.25rem;
  border-radius: 0.3125rem;
  cursor: pointer;
}

button:hover {
  background-color: #5d085d;
}
</style>
