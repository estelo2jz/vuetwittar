<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">
        @{{ user.username }}
      </h1>
      <!-- v-if="follower > 10" then show this -->
      <div class="user-profile__admin-badge" v-if="user.isAdmin">
        Admin
      </div>
      <!-- <div class="user-profile__admin-badge" v-if="!user.isAdmin">
        Not Admin
      </div> -->
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      </div>
    </div>
    <div class="user-profile__tweets-wrapper">
      <!-- or  v-for="(tweet, index) in user.tweets" -->
      <TweetItem v-for="tweet in user.tweets" :key="tweet.id" :username="user.username" :tweet="tweet" />
    </div>
  </div>
</template>

<script>
import TweetItem from './TweetItem';

export default {
  name: 'UserProfile',
  components: {
    TweetItem
  },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: 'estelo2jz',
        firstName: "Estelo",
        lastName: 'Abellanosa',
        emaiL: "estelo2jz@space.com",
        isAdmin: true,
        tweets: [
          { id: 0, content: "CyberOunk 2077 is 9 days away!" },
          { id: 1, content: "PS5 is better than XBOX!" },
        ]
      }

    }
  },
  // watch, it watches a  data point, and when it changes you can add a function.
  // here were watching on the followers, so we can do something when somebody follow us.
  // what the data is now, and what i'ts used to be.
  // when the data changes you can gonna pass two variables, you gonna passed "what the data is now" and "what is used to be".
  // Is saying hey "if the old email is deffirent from the new email run something".
  // really useful to compare the OLD and the NEW.
  watch: {
    followers(newFollowerCount, oldFollowerCount) { 
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!`)
      }
    }
  },
  // computed property
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`
    }
  },
  // function we created wiil be here
  methods: {
    followUser() {
      this.followers++
      // this.followers = this.followers + 1
      // this.followers += 1
    }
  },
  // mount is gonna run when we first load the component
  // this will follow you instantly
  mounted() {
    this.followUser();
  }
}
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 80;
  padding: 50px 5%;
}
.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  text-align: left;
}
.user-profile__admin-badge {
  background-color: purple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 5px 10px;
  font-weight: bold;
}
h1 {
  margin: 10px 0px;
}
</style>
