<template>
 <div>
  
  <Autos/>

 </div>
</template>

<script>
 import Autos from './components/Autos.vue'


export default {
  name: 'App',
  components: {
    Autos

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
