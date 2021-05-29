<template>
<div class= "tweetBox" v-if="registered">
  <div class="card">
    <h2>Welcome {{userData.name}} write your first Tweet</h2>
    <form v-on:submit.prevent="sendTweet">
      <div class="form_group">
        <label for="tweet">Send your tweet
          <span>{{ tweetMsg.length + '/' + max_tweet }}</span>
        </label>
        <textarea name="tweet" id="tweet" cols="30" rows="10" v-model="tweetMsg" maxlength="200"></textarea>
      </div>
      <button type="submit">Tweet</button>
    </form>
  </div>
</div>


</template>

<script>
export default {
  name: 'Register',
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
    sendTweet (){
      this.tweets.unshift(
        {
          text: this.tweetMsg,
          date: new Date().toLocaleString()
        }
      )
      this.tweetMsg = ''
      
      let stringTweets = JSON.stringify(this.tweets)
      localStorage.setItem('simple_tweet_tweets', stringTweets)

    },
    registerAccount(){
      if(this.name !=='' && this.email !=='' && this.password !==''){
        this.userData.id = ++this.usersID
        this.userData.name= this.name
        this.userData.email = this.email
        this.userData.password = this.password
      }
      else{
        this.error = 'Complet all the form fields'
      }

      localStorage.setItem('simple_tweet_registered',true)
      localStorage.setItem('simple_tweet_registered_user', JSON.stringify(this.userData))

      this.name=''
      this.email=''
      this.password=''

    }
  },
  created(){
    const registeredUser = localStorage.getItem('simple_tweet_registered_user')
    const registered = localStorage.getItem('simple_tweet_registered')
    if(registered === 'true') {
      this.registered = true
    }
    if(registeredUser){
      this.userData = JSON.parse(registeredUser)
    }
  }
}
</script>