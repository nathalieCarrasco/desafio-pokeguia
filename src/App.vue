<template>
  <div id="app">
    <img id="logopoke" src="./assets/pokemon-logo.jpg">
  <pokeguiapp />
  </div>
</template>

<script>
import Pokeguiapp from './components/Pokeguiapp.vue'


export default {
  name: 'App',
  components: {
    Pokeguiapp
  
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000000;
  margin-top: 60px;
  background-color: aliceblue;
}

#logopoke{
  width: 500px;
  margin: 0;
  padding: 0;
}
html{
  background-image: url(https://i.pinimg.com/564x/c1/9c/cd/c19ccd7acbe27e8acbcdae7c07b3646e.jpg);
}
</style>
px