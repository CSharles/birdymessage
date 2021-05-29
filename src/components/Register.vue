<template>
<div class="card">
  <font-awesome-icon icon="twitter" size="lg" fixed-width />
  <h2>Create your account</h2>
  <div class="register" v-if="!registered">
    <form v-on:submit.prevent="registerAccount()">
      <div class="form_group">
        <label for="name">Name</label>
        <span>{{name.length +'/'+max_length}}</span>
        <input type="text" v-model="name" :maxlength="max_length" required>
      </div>
      <div class="form_group">
        <label for="email">Email</label>
        <span>{{email.length +'/'+max_length}}</span>
        <input type="email" v-model="email" :maxlength="max_length" required>
      </div>
      <div class="form_group">
        <label for="password">Password</label>
        <span>{{password.length +'/'+max_pass_length}}</span>
        <input type="email" v-model="password" :maxlength="max_pass_length" required>
      </div>
      <button type="submit">Register</button>
    </form>
    <div v-if="error.length > 0">{{ error }}</div>
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
    }
  },
  methods:{
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

