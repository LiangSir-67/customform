<template>
  <div id="app">
    <cloneForm></cloneForm>
  </div>
</template>

<script>
import cloneForm from './components/CloneForm.vue'

export default {
  name: 'app',
  components: {
    cloneForm
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
}
</style>
