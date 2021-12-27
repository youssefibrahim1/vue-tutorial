<template>
<div id="app">
  <UserProfile/>
</div>
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* margin-top: 60px; */
  color: #2c3e50;
  display: flex;
    justify-content: center;
  align-items: center;
  flex-direction: column;
}

#btn-follow{
  width: 100px;

}
</style>
