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
        <form class="user-profile_create-twoot" @submit.prevent="createNewTwoot">
          <label for="newTwoot"><strong>New Twoot</strong></label>
          <textarea id="newTwoot" rows="4" v-model="newTwootContent"></textarea>
          <div class="user-profile_create-twoot-type">
            <label for="newTwootType"><strong>Type: </strong> </label>
            <select id="newTwootType" v-model="selectedTwootType">
              <option :value="option.value" v-for="(option, idx) in twootTypes" :key="idx">
                {{option.name}}
              </option>
            </select>
          </div>
                  <button>
          Twoot
        </button>
        </form>

          <!-- <button id="btn-follow" @click="followUser">Follow</button> -->
    </div>
    <div class="user-profile_twoots-wrapper">
      <TwootItem v-for="twoot in user.twoots" :key="twoot.id" :username="user.username" 
      :twoot="twoot" @favorite="toggleFavorite"/>
        
    </div>
</div>
</template>

<script>
import TwootItem from "./TwootItem.vue"

export default {
  name: 'UserProfile',
  components: {TwootItem},
  data() {
    return {
      newTwootContent: '',
      selectedTwootType: '',
      twootTypes: [
        {
          value: 'draft',
          name: 'Draft',
        },
        {
          value: 'Instant',
          name: 'Twoot',
        },
      ],
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
    },
    toggleFavorite(id){
      console.log(`Favorited Tweet ${id}`);
    },
    createNewTwoot(){
      if(this.newTwootContent && this.selectedTwootType !== 'draft'){
        this.user.twoots.unshift({
          id:this.user.twoots.length + 1,
          content: this.newTwootContent
        })
        this.newTwootContent = ""
      }
    }
  },
  mounted(){
      this.followUser()
  },
}
</script>

<style lang="scss" scoped>
.user-profile{
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;

    .user-profile_user-panel {
      display: flex;
      flex-direction: column;
      margin-right: 50px;
      padding: 20px;
      background-color:white;
      border-radius: 5px;
      border: 1px solid #DEF3E8;

        h1{
          margin: 0;
        }
    }

    .user-profile_admin-badge{
      background: rebeccapurple;
      color: white;
      border-radius: 5px;
      margin-right:auto;
      padding: 0 10px;
      font-weight: bold;
    }

    .user-profile_twoots-wrapper{
      display: grid;
      grid-gap: 10px;
    }
}

.user-profile_create-twoot{
  display: flex;
  flex-direction: column;
  border-top: 1px solid black;
  padding-top: 20px
}

</style>
