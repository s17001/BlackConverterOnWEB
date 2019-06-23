<template>
  <div id="app">
    <!--<HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <Converter />
    <div style="text-align: right">
      <small >作った人 : <a href="https://twitter.com/Ryu1__1uyR">Ryu</a></small>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Converter from './components/Converter.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Converter
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
a{
  text-decoration: none;
  color: #42b983;
}
a:hover{
  color: steelblue;
}
</style>
