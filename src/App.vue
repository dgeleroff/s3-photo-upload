<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view/>
    <uploader></uploader>
  </div>
</template>

<script>
import Uploader from '@/components/Uploader.vue'
export default {
  name: 'App',
  components: {
    Uploader
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
