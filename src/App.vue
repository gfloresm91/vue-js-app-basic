<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>Bienvenido a Vue music con last.fm api</h1>
    <h2>Top artistas en Chile</h2>
    <topartistas v-for="artista in artistas" :artista="artista" :key="artista.mbid"></topartistas>
  </div>
</template>

<script>
import topartistas from './components/topartistas.vue'
import getArtists from './api'

export default {
  name: "app",
  data() {
    return {
      artistas: []
    }
  },
  components:{
    topartistas
  },
  mounted: function(){
    const self = this
    getArtists()
      .then(function(artistas){
        self.artistas = artistas
      })
  }
}
</script>

<style lang="stylus">
#app
  font-family "Avenir", Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px

h1,
h2
  font-weight normal

ul
  list-style-type none
  padding 0

li
  display inline-block
  margin 0 10px

a
  color #42b983
</style>
