<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <WrapScroll :items="items" :width="1152"></WrapScroll>
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
  },
  data(){
    return{
      items:[
        {imageUrl:[require("./assets/1 (1).png")],nickname:'aaaa'},
        {imageUrl:[require("./assets/1 (2).png")],nickname:'qqqqq'},
        {imageUrl:[require("./assets/1 (3).png")],nickname:'wwwww'},
        {imageUrl:[require("./assets/1 (4).png")],nickname:'eeeee'},
        {imageUrl:[require("./assets/1 (5).png")],nickname:'atttttaaa'},
        {imageUrl:[require("./assets/1 (6).png")],nickname:'aayyyyaa'},
        {imageUrl:[require("./assets/1 (7).png")],nickname:'yyyy'},
        {imageUrl:[require("./assets/1 (8).png")],nickname:'aauuuuaa'},
        {imageUrl:[require("./assets/1 (9).png")],nickname:'uuuu'}
      ]
    }
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
