<template>
  <div>
     <div class="col-md-5" style="background-color: white; padding: 60px; border: 1px solid #e6e6e6;">
      <h3 class="text-center" style="margin-top:0">Bacaan Baik</h3>
      <p class="text-center" style="color:#999;font-weight:700;font-size:17px;line-height:20px;">Sign In to see and post great books</p>
      <div class="form-group">
        <input type="text" class="form-control" v-model="email" placeholder="Email">
      </div>
      <div class="form-group">
        <input type="password" class="form-control" v-model="password" placeholder="Password">
      </div>
      <div class="form-group">
        <button type="submit" class="btn btn-default" @click="checkLoginStatus" style="width:100%;background-color:#3897f0;color:white;"><b>Sign In</b></button>
      </div>
      <p class="text-center" style="color:#999;font-weight:700;font-size:14px;line-height:18px;">
          By signing up, you agree to our <br> <b style="color:#000">Terms</b> & <b style="color:#000">Privacy Policy</b>.
      </p>
      <br>
      <p class="text-center">
          New to Bacaan Baik? <a @click="changeToRegister" style="cursor: pointer;">Sign Up</a>
      </p>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios'
export default {
  name: 'TemplateLogin',
  data() {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    checkLoginStatus () {
      let self = this
      axios
        .post('http://localhost:3000/users/login', {
          username: this.email,
          password: this.password
        })
        .then( function (response) {
          if (response.data.token){
            localStorage.setItem('token', response.data.token)
            localStorage.setItem('user', response.data.fullname)
            localStorage.setItem('email', response.data.username)
            localStorage.setItem('id', response.data.id)
            self.$router.push({name: 'mainpage'})
          }
        })
        .catch( function (err) {
          console.log(err)
        })
    },
    changeToRegister () {
      this.$router.push({name: 'home'})
    }
  }
}
</script>

<style>

</style>
