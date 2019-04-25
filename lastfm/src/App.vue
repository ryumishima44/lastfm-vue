<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 Last FM vue
    select(v-model='selectedCountry')
      option(v-for='country in countries' v-bind:value='country.value') {{ country.name }}
    ul
      artist(v-for='artist in artists' v-bind:artist="artist" v-bind:key="artist.mbid")
</template>

<script>
  import Artist from './components/Artist.vue'
  import getArtists from './api'
  export default {
    name: 'app',
    data () {
      return {
        artists: [],
        countries: [
          {name:'España', value:'spain'},
          {name:'Colombnia', value:'colombia'},
          {name:'Argentina', value:'argentina'}
        ],
        selectedCountry:'spain'
      }
    },
    components: {
      Artist
    },
    methods: {
      refreshArtists() {
      const self = this
      getArtists(this.selectedCountry)
      .then(function(artists) {
        self.artists = artists
      })
      }
    },
    watch: {
      selectedCountry: function() {
        this.refreshArtists()
      }
    },
  }
</script>

<style lang="stylus">
#app
    font-family 'Avenir', Helvetica, Arial, sans-serif
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
    text-align center
    color red
    margin-top 60px

h1, h2
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
