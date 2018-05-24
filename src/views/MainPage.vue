<template>
  <div>
    <TopNavBar/>
    <br>
    <TemplateMainPage/>
  </div>
</template>

<script>
/* eslint-disable */
import TemplateMainPage from '@/components/TemplateMainPage.vue'
import TopNavBar from '@/components/TopNavBar.vue'
export default {
  name: 'MainPage',
  components: {TemplateMainPage, TopNavBar},
  beforeCreate () {
    if(!localStorage.getItem('token')){
      this.$router.push({name:'home'})
    }
  }
}
</script>

<style>

</style>
