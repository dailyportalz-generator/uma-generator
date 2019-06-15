<template>
  <div id="app">
    <Header />
    <Questions v-if="!showResult" />
    <Result v-if="showResult" />
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import Questions from './components/Questions'
import Result from './components/Result'

export default {
  name: 'app',
  data() {
    return {
      showResult: true
    }
  },
  components: {
    Header,
    Footer,
    Questions,
    Result,
  },
  methods: {

  }
}
</script>

<style>
* {
  box-sizing: border-box;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 640px;
  font-size: 12px;
  padding: 0 50px;
}
</style>
