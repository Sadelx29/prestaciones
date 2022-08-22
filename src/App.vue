<template>
<div>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <ForM></ForM>
  <PriMer></PriMer>
</div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

import PriMer from './components/primer.vue'
import ForM from './components/formulario.vue'
export default {
  name: 'App',
  components: {
    HelloWorld,
    PriMer,
    ForM
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
