<template>
  <div id="app">
    <Register />
    <TweetBox />
  </div>
</template>

<script>
import Register from './components/Register'
import TweetBox from './components/TweetBox'

export default {
  name: 'App',
  components: {
    Register,
    TweetBox
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
