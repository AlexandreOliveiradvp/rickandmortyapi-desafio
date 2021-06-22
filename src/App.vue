<template>
  <div id="app">
    <Header/>
    <Section_first/>
    <Section_second/>
    <Footer/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Section_first from './components/Section_first.vue'
import Section_second from './components/Section_second.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    Section_first,
    Section_second,
    Footer,
  
  }
}
</script>

<style>
#app {
  font-family: 'Merriweather Sans', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
