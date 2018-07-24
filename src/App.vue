<template>
  <div id="app">
    <router-view/>
    <footer>
      <p>Made by <a href="#">Rach</a> &amp; <a href="#">Steve</a></p>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}

footer {
  margin-top: 20px;
  background-color: rgba(0,128,128, .8);
  padding: 20px 0;
  color: white;
  font-weight: bold;
  font-size: 18px;
}

footer p {
  text-align: center;
}

footer p a:link, footer p a:visited {
  color: white;
}
</style>
