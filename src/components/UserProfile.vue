<template>
  <div id="app">
    <div class="user-profile">
      <div class="user-profile__user-panel">
        <h1 class="user-profile__username">@{{ user.username }}</h1>
        <div class="user-profile__verificated-badge" v-if="user.isVerificated">
          Verificated
        </div>
        <div class="user-profile_follower-count">
          <strong>Followers: </strong> {{ followers }}
        </div>

        <button @click="followMe" id="follow_button">Follow</button>

        <form class="user-profile__create-twet" @submit.prevent="createNewTwit">
          <label for="newTwet"><strong>New Twit</strong></label>
          <textarea id="newTwit" rows="4" v-model="newTwitContent"></textarea>

          <div class="user-profile__create-twit-type">
            <label for="newTwitType"><Strong>Type:</Strong></label>
            <select name="" id="newTwitType" v-model="selectedTwitType">
              <option
                :value="option.value"
                v-for="(option, index) in TwitTypes"
                :key="index"
              >
                {{ option.name }}
              </option>
            </select>
          </div>
          <button>Twit</button>
        </form>
      </div>

      <div class="user-profile__twits-wrapper">
        <TwitItem
          v-for="twit in user.twits"
          :key="twit.id"
          :username="user.username"
          :twit="twit"
          @favourite="toggleFavourite"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TwitItem from "./TwitItem.vue";

export default {
  name: "UserProfile",

  components: {
    TwitItem,
  },

  props: {
    msg: String,
  },

  data() {
    return {
      newTwitContent: "",
      selectedTwitType: "instant",
      TwitTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Twit" },
      ],
      followers: 123,
      followed: false,
      user: {
        id: 1,
        username: "n1sb0",
        firstname: "Bohdan",
        lastname: "Sivak",
        email: "bohdan.sivak@gmail.com",
        isVerificated: true,
        twits: [
          { id: 1, content: "This is my first Twet" },
          { id: 2, content: "Today is a great day!" },
          { id: 3, content: "You!!! how are you :)" },
          { id: 4, content: "Awsome post with simple text" },
        ],
      },
    };
  },

  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!`);
      } else {
        console.log(`${this.user.username} losse a follower!`);
      }
    },
  },

  methods: {
    followMe() {
      var btn = document.getElementById("follow_button");

      if (this.followed) {
        this.followers--;
        btn.innerHTML = "Follow";
      } else {
        this.followers++;
        btn.innerHTML = "UnFollow";
      }

      this.followed = !this.followed;
    },

    toggleFavourite(id) {
      console.log(`FAVOURITED Twit #${id}`);
    },

    createNewTwit() {
      if (this.newTwitContent && this.selectedTwitType !== "draft") {
        this.user.twits.unshift({
          id: this.user.twits.length + 1,
          content: this.newTwitContent,
        });
      }
      this.newTwitContent = "";
    },
  },

  computed: {
    newTwitCharacterCount(){
      return this.newTwitContent.length;
    },

    fullName() {
      return `${this.user.firstname} ${this.user.lastname}`;
    },
  },

  mounted() {},
};
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  padding: 50px 5%;

  .user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    border-radius: 5px;
    border: 1px solid #e5e5e5;
    background-color: white;

    h1 {
      margin: 0;
    }

    .user-profile__username {
      margin-right: auto;
      margin-bottom: 10px;
    }

    .user-profile__verificated-badge {
      background: #42b983;
      color: white;
      border-radius: 5px;
      margin-right: auto;
      margin-bottom: 5px;
      padding: 0 10px;
      font-weight: bold;
    }

    .user-profile__create-twet {
      display: flex;
      flex-direction: column;
      margin-top: 15px;
      border-top: 1px solid #333;
      padding-top: 15px;
    }

    .user-profile__create-twit-type {
      margin-top: 15px;
    }
  }
}

button {
  background: #2c3e50;
  border: 0;
  color: aliceblue;
  font-size: 1.2rem;
  outline-style: none;
  cursor: pointer;
  margin-top: 15px;
  border-radius: 5px;
  height: 30px;
}

button:hover {
  background: #44bba4;
}

label{
  color: aliceblue;
  font-size: 1.2rem;
  outline-style: none;
  margin-top: 15px;
  border-radius: 5px;
  height: 30px;
}
</style>
