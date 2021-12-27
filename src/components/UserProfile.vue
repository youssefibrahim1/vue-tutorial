<template>
<div class="user-profile">
    <div class="user-profile_user-panel">
        <h1 class="user-profile_username">@{{user.username}}</h1>
        <div class="user-profile_admin-badge" v-if="user.isAdmin">
          Admin
        </div>
        <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
        <div id="user-profile_follower-count">
            <strong> Followers: {{followers}}</strong>
        </div>
            <button id="btn-follow" @click="followUser">Follow</button>
    </div>
    <div class="user-profile_twoots-wrapper">
      <div class="user-profile_twoot" v-for="twoot in user.twoots" :key="twoot.id">
        {{twoot.id}}. {{ twoot.content }}
      </div>
    </div>
</div>
</template>

<script>

export default {
  name: 'UserProfile',
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "youssefibrahim",
        firstName: "Youssef",
        lastName: "Ibrahim",
        email: process.env.GMAIL,
        isAdmin: true,
        twoots: [
          {
            id:1,
            content: "Twotter is Amazing"
          },
          {
            id:2,
            content: "Like and subscribe"
          }
        ]
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount){
      if(oldFollowerCount < newFollowerCount){
        console.log(`${this.user.username} has gained a follower`);
      }
    }
  },
  computed: {
    fullName(){
      return `${this.user.firstName} ${this.user.lastName}`
    }
  },
  methods: {
    followUser() {
      this.followers++
    }
  },
  mounted(){
      this.followUser()
  },
  components: {
  }
}
</script>

<style>
.user-profile{
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
}

.user-profile_user-panel {
    display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color:white;
  border-radius: 5px;
  border: 1px solid #DEF3E8;
}

h1{
  margin: 0;
}

.user-profile_admin-badge{
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right:auto;
  padding: 0 10px;
  font-weight: bold;
}

</style>
