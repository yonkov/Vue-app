<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>We are two seasoned WordPress professionals, who used to work at <a href="https://webfactory.bg/">WebFactory BG</a> - <br> a legendary company with more than 20 years of experience in the IT field.<br><br>
    We finally found the courage to kickstart on our own and this is our brand new product - Nasio Themes. <br>
      Reach out to our huge collection of high quality free and premium WordPress themes. <br><br> Nasio Themes are the only WordPress themes you will ever need.<br>
      For more information check out Nasio Themes's
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener"> documentation</a>.<br><br>
      PS: Sometimes we get bored of WordPress and then we develop beautifus SPA using cutting edge technologies,<br> such as React.js, Angular.js and of course Vue.js.
      This website is poudly powered by Vue.js.
    </p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
nav > * {
    margin: 5px;
}
</style>