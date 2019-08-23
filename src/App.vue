<template>
  <div id="app">
    <Header/>
    <Navigation/>
    <main>
    <router-view msg="Welcome to Nasio Themes"></router-view>
    </main>
    <Footer/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Navigation from './components/Navigation.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'app',
  components: {
    Header,
    Navigation,
    Footer 
  }
}
</script>

<style>
html {
    position: relative;
    min-height: 100%;
}
body {
    margin: 0 0 100px; /* bottom = footer height */
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#app img{
  width: 250px;
}
nav >*{
  margin:5px;
}
</style>