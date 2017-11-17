<template>
  <li>
    <h2>
      <a :href="artist.url" target="_blank">{{ artist.name }}</a>
    </h2>
    <img :src="artist.image[2]['#text']" alt="">
  </li>
</template>

<script>
  export default {
    // Debe coincidir con el tag <artist>
    name: 'artist',
    // Propiedades que recibe
    // el artist del array hace referencia al v-bind:artist="artist"
    props: ['artist']
  }
</script>

<!--
  scoped = reduce el alcance de los estilos, funciona como un namespace
  Así no se pisan los estilos de otros componentes
-->

<style lang="sass" scoped>
li
  display: inline-block
  margin: 5px 10px
</style>
