<template>
  <li>
    <base-card>
      <header>
        <h1>{{ module }}</h1>
        <section>
          <font-awesome-icon :icon="faTrashCan" class="delete" />
          <font-awesome-icon :icon="faPenToSquare" class="edit" />
        </section>
      </header>
      <p>{{ content }}</p>
      <p>Duration: {{ duration }}</p>
    </base-card>
  </li>
</template>

<script setup>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faTrashCan, faPenToSquare } from '@fortawesome/free-solid-svg-icons'
const { module, content, duration } = defineProps(['module', 'content', 'duration'])
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
</style>
