<template>
<div>
  <div class="col-md-5" style="background-color: white; padding: 60px; border: 1px solid #e6e6e6;">
    <h3 class="text-center" style="margin-top:0">Bacaan Baik</h3>
    <p class="text-center" style="color:#999;font-weight:700;font-size:17px;line-height:20px;">Sign Up to see and post great books</p>
    <div class="form-group">
      <input type="text" class="form-control" v-model="fullname" placeholder="Full Name">
    </div>
    <div class="form-group">
      <input type="text" class="form-control" v-model="email" placeholder="Email">
    </div>
    <div class="form-group">
      <input type="password" class="form-control" v-model="password" placeholder="Password">
    </div>
    <div class="form-group">
      <button type="submit" class="btn btn-default" @click="registerUser" style="width:100%;background-color:#3897f0;color:white;"><b>Sign Up</b></button>
    </div>
    <p class="text-center" style="color:#999;font-weight:700;font-size:14px;line-height:18px;">
        By signing up, you agree to our <br> <b style="color:#000">Terms</b> & <b style="color:#000">Privacy Policy</b>.
    </p>
    <br>
    <p class="text-center">
        Have an account? <a @click="changeLogin" style="cursor: pointer;">Log in</a>
    </p>
  </div>
</div>
</template>

<script>
/* eslint-disable */
import axios from 'axios'
export default {
  name: 'TemplateSignup',
  data () {
    return {
      fullname: '',
      email: '',
      password: ''
    }
  },
  methods: {
    registerUser () {
      let self = this
      axios 
        .post('http://localhost:3000/users/register', {
        fullname: this.fullname,
				username: this.email,
				password: this.password
        })
        .then(response => {
          if(response.data.result !== undefined) {
            self.$router.push({name: 'login'})
          }
        })
        .catch(err => {
          console.log(err)
        })
      
    },
    changeLogin () {
      this.$router.push({name: 'login'})
    }
  }
}
</script>

<style>
.col-md-5{width:100%;margin:0 auto;text-align:left;}
</style>
