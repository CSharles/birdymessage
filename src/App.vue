<template>
  <div id="app">
    <div class="card tex-center">
      <font-awesome-icon :icon="['fab', 'twitter']" size="lg" fixed-width />
      <Register />
      <TweetBox />
    </div>
      <TweetList />
  </div>
</template>

<script>
import Register from './components/Register'
import TweetBox from './components/TweetBox'
import TweetList from './components/TweetList'

export default {
  name: 'App',
  components: {
    Register,
    TweetBox,
    TweetList
  }
}
</script>
