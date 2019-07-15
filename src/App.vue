<template>
  <div id="app">
    <Header></Header>
    <div class="row" v-for="format in listDecks" v-bind:key="format.did">
        <div class="col s12 m6">
          <div class="card deep-purple">
            <div class="card-content white-text">
              <span class="card-title">{{format.name}}</span>
              <p>Descrição do Formato</p>
            </div>
            <div class="card-action align-right">
              <a href="#">Metagame</a>
            </div>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
import Header from './components/layout/Header.vue'
import axios from 'axios'
import { parse } from 'path';

export default {
  name: 'app',
  components: {
    Header
  },
  data () {
    return {
      formats: null
    }
  },
  async created() {
    try {
      const res = await axios.get('https://mtgmeta.io/api/decks/pauper')
      this.formats = res.data
    } catch(e) {
      console.log(e)
    }
  },
  computed: {
    listDecks() {
      return this.formats.data.sort((a, b) => {
        if (a.metashare > b.metashare)
        return -1;
      if (a.metashare < b.metashare)
        return 1;
      return 0;
      })
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
