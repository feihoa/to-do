<template>
  <div id="app">
    <h1 class="app__header">Приложение</h1>
    <hr>
    <router-view/>
  </div>
</template>



<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}
.app__header{
  margin-top:0px;
}


</style>

<script>

export default {
    name: 'App',
}
</script>