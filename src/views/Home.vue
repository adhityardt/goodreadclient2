<template>
  <div class="home">
    <h1>SignUp Page</h1>
    <TemplateSignup/>
  </div>
</template>

<script>
// @ is an alias to /src
import TemplateSignup from '@/components/TemplateSignup.vue'

export default {
  name: 'home',
  data () {
    return {

    }
  },
  components: {
    TemplateSignup
  },
  beforeCreate () {
    if (localStorage.getItem('token')){
      this.$router.push({name: 'mainpage'})
    }
  }
}
</script>
