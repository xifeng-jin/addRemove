<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld title="Welcome To My First Vue Project"/>
    <Form/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Form from  './components/xx.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Form
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
  margin-top: 10px;
}
</style>
