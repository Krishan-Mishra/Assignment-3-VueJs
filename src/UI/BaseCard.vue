<template>
  <div><slot> </slot></div>
</template>

<style scoped>
div {
  border-radius: 0.75rem;
  box-shadow: 0 0.125rem 0.5rem rgba(0, 0, 0, 0.9);
  padding: 1rem;
  margin: 2rem auto;
  max-width: 40rem;
}
div {
  -webkit-transition-duration: 0.3s;
  transition-duration: 0.3s;
  -webkit-transition-property: transform;
  transition-property: transform;
}
div:hover {
  -webkit-transform: scale(0.8);
  transform: scale(0.97);
}
</style>
