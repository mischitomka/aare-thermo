<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld :temp='temp' :datum='datum' msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    HelloWorld
    },
   data: function () {
         return {temp:20, datum:''}
        },
  mounted () {
          axios
              .get('https://www.wiewarm.ch:443/api/v1/temperature.json/17')
              .then((response) => {
                  this.temp = parseFloat(response.data['52']['temp'])
                  this.datum = (new Date(Date.parse(response.data['52']['date']))).toLocaleDateString('de-CH',{ day: '2-digit', month: '2-digit',year: 'numeric', hour: '2-digit', minute: '2-digit'  })
              })
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
