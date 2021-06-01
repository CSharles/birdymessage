<template>
  <div class="card_tweets"  v-if="registered">
    <section class="tweets" v-if="tweets.length >0">
      <h2>Tweets</h2>
      <div class="tweetMsg" v-for="(tweet, index) in tweets" :key="index">
        <p>
          {{tweet.text}}
        </p>
        <div class="tweetDate">
            <font-awesome-icon icon="calendar-alt" size="sm" fixed-width />
            {{tweet.date}}
        </div>
        <div class="tweet_remove" @click="removeTweet(index)">
          <span class="remove">Delete this tweet
            <font-awesome-icon icon="trash" size="xs" fixed-width />
          </span>
        </div>
      </div>
    </section>
    <div v-else>No tweets to show</div>
  </div>
</template>

<script>
export default {
  name: 'TweetList',
  data() {
     return {
      userData:{},
      usersID: 0,
      name:'',
      email:'',
      password:'',
      max_length:25,
      max_pass_length:16,
      registered: false,
      error:'',
      tweetMsg:'',
      max_tweet:200,
      tweets:[]
    }
  },
  methods:{
    removeTweet(index){
      let removeIt = confirm('Are you sure you want to remove this tweet?')
      if(removeIt) {
        this.tweets.splice(index,1)
        localStorage.simple_tweet_tweets = JSON.stringify(this.tweets)
      }
    }
  },
  created(){
    const registeredUser = localStorage.getItem('simple_tweet_registered_user')
    const registered = localStorage.getItem('simple_tweet_registered')
    let tweets = localStorage.getItem('simple_tweet_tweets')
    if(registered === 'true') {
      this.registered = true
    }
    if(registeredUser){
      this.userData = JSON.parse(registeredUser)
    }
    if(tweets){
      console.log('there is a list of tweets');
      this.tweets = JSON.parse(tweets)
    }
    else{
      console.log('No tweets here');
    }
  }
}
</script>