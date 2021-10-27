<template>
  <div id="app">
    <filesystem :directory="directory" :max-level="2"/>
  </div>
</template>

<script>
import JSON from '../public/static/node_modules.json'
import filesystem from './components/filesystem.vue'

export default {
  name: 'App',
  components: {
    filesystem
  },
  data() {
    return {
      directory: JSON
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300&display=swap');

#app {
  font-family: 'Montserrat', sans-serif;
}
</style>
