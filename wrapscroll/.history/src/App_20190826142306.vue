<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <wrap-scroll></wrap-scroll>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import WrapScroll from './components/wrapScroll.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    WrapScroll
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
