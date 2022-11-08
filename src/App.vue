<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HomeView msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HomeView from './components/HomeView.vue'

export default {
  name: 'App',
  components: {
    HomeView
  }
}
</script>

<style>
body{
  margin:0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #f0e7e7;
  background-color: #2c3e50;
  height: 100vh;
}
</style>
