<template>
  <div id="app">
    <Header></Header>
    <div></div>
  </div>
</template>

<script>
import Header from './components/layout/Header.vue'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    Header
  },
  data () {
    return {
      decks: null
    }
  },
  async created() {
    try {
      const res = await axios.get('http://mtgmeta.io/api/decks/', {crossdomain: true})
      this.decks = res.data
    } catch(e) {
      console.log(e)
    }
  }
    
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
