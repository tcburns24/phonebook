
<script>
import Phonebook from './components/Phonebook.vue'

export default {
  name: 'App',
  components: {
    Phonebook
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<template>
  <div id="app">
    <Phonebook />
  </div>
</template>