<template>
  <div id="app">
    <NavMenu></NavMenu>
    <div class="app-main">
      <router-view></router-view>
    </div>
    <Footer></Footer>
  </div>
</template>

<script>
import Footer from '@/components/Footer.vue'
import NavMenu from '@/components/NavMenu.vue'
import ScatterJS from 'scatterjs-core'
import ScatterEOS from 'scatterjs-plugin-eosjs'
// import { API_URL } from '@/assets/constants.js'
// import { connect } from 'http2'

ScatterJS.plugins(new ScatterEOS())
export default {
  name: 'app',
  components: {
    Footer,
    NavMenu
  },
  created () {
    this.$store.dispatch('getAccounts')
    this.$store.dispatch('getProposals')
    this.$store.dispatch('getVotes')
    this.$store.dispatch('getProxies')
    ScatterJS.scatter.connect('My-App').then(connected => {
      if (!connected) return false
      // 有scatter
      this.$store.dispatch('setScatter', { scatter: ScatterJS.scatter })
    })
  },
  methods: {
  }
}
</script>

<style scope>
body {
  margin: 0;
  background-color: rgb(232,236,255);
}

.app-main {
  min-height: calc(100vh - 160px - 60px);
  background-color: rgb(232,236,255);
  max-width: 1420px;
  margin: auto
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
