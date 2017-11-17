<template>
  <div id="app">
    <img src="https://jhonatanc.github.io/platzi-music/dist/logo.png">
    <h1>Platzi Music</h1>
    <select v-model="selectedCountry" id="">
      <option v-for="country in countries" :value="country.value">
        {{ country.name }}
      </option>
    </select>
    <spinner v-show="loading"></spinner>
    <ul>
      <!--<li v-for="artist in artists">{{ artist.name }}</li>-->
      <artist v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid">
        {{ artist.name }}
      </artist>
    </ul>
  </div>
</template>

<script>

// Importantdo el componente
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'

import getArtists from '../api'

export default {
  name: 'app',
  data () {
    return {
      //msg: 'Welcome to Your Vue.js App'
      /*artists: [
        { name: 'Angel Bonne'},
        { name: 'Angel Canales'},
        { name: 'Ismael Miranda'},
      ]*/
      artists: [],
      countries: [
        { name: 'Argentina', value: 'argentina' },
        { name: 'Colombia', value: 'colombia' },
        { name: 'España', value: 'spain' }
      ],
      selectedCountry: 'colombia',
      loading: true
    }
  },

  // Decirle a la vista que componente va a utilizar
  components: {
    // Artist: Artist
    // Como es el mismo nombre del componente se puede usar sólo Artist
    Artist,
    Spinner
  },
  methods: {
    refreshArtists(){
      const self = this
      this.loading = true
      this.artists = []
      getArtists(this.selectedCountry)
        .then(function(artists){
          self.loading = false
          self.artists = artists
        })
    }
  },

  // funcion que se ejecuta cuando ya están todos los elementos en el DOM
  mounted: function(){
    /*const self = this
    getArtists()
      .then(function(artists){
        self.artists = artists
      })*/
    this.refreshArtists()
  },
  watch: {
    selectedCountry: function(){
      /*const self = this
      getArtists()
        .then(function(artists){
          self.artists = artists
        })*/
      this.refreshArtists()
    }
  }
}
</script>

<style lang="sass">
#app
  font-family: 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  margin-top: 60px

h1, h2
  font-weight: normal

ul
  list-style-type: none
  padding: 0

li
  display: inline-block
  margin: 0 10px

a
  color: #42b983

</style>
