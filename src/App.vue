<template>
  <div id="app">
    <TextEditor msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import TextEditor from './components/TextEditor.vue'

export default {
  name: 'App',
  components: {
    TextEditor
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
