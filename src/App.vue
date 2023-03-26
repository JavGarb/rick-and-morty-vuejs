<template>
  <div>
  <NavBar />
  <HelloWorld msg="Rick And Morty App in Vuejs"/>
  <div>
    <Cards />
  </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import NavBar from './components/NavBar.vue'
import Cards from './components/Cards.vue'
export default {
  name: 'App',
  components: {
    HelloWorld,
    NavBar,
    Cards,
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
  margin: 0;
  padding: 0;
}
</style>
