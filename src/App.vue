<template>
  <UserProfile msg = "Hello"/>
</template>

<script>
import UserProfile from './components/UserProfile.vue'

export default {
  name: 'App',

  components: {
    UserProfile
  }
}
</script>

<style>
html {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: #F3F5FA;
}

</style>
