<template>
  <div class="navbar">
    <p class="navbar-logo">Twotter</p>
    <p class="navbar-username">{{ user.username }}</p>
  </div>
  <div class="user-profile">
    <div class="user-profile_user-panel">
      <h1 class="user-profile_username">@{{ user.username }}</h1>
      <h2>{{ user.id }}</h2>
      <div class="user-profile_admin-badge" v-if="user.isAdmin">
        Admin
      </div>
      <div class="user-profile_admin-badge" v-else>
        NOT Admin
      </div>
      <div class="user-profile_follower-count">
        <strong>Followers:</strong>{{ followers }}
      </div>
      <form
        class="user-profile_create-twoot"
        @submit.prevent="createNewTwoot"
        :class="{ '--exceded': newTwootCharacterCount > 180 }"
      >
        <label for="newTwoot"
          ><strong>New Twoot</strong> ({{ newTwootCharacterCount }}/180)</label
        >
        <textarea
          name="newTwoot"
          id="newTwoot"
          cols="30"
          rows="4"
          v-model="newTwootContent"
        ></textarea>

        <div class="user-profile_create-twoot-type">
          <label for="newTwootType"><strong>Type:</strong></label>
          <select id="newTwootType" v-model="selectedTwootType">
            <option
              :value="option.value"
              v-for="(option, index) in twootTypes"
              :key="index"
            >
              {{ option.name }}
            </option>
          </select>
        </div>
        <button class="user-profile_twoot-button">
          Twoot!
        </button>
      </form>
    </div>
    <div class="user-profile_twoots-wrapper">
      <TwootItem
        v-for="twoot in user.twoots"
        :key="twoot.id"
        :username="user.username"
        :twoot="twoot"
        @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>

<script>
import TwootItem from "../TwootItem";
import { useRoute } from "vue-router";
export default {
  name: "UserProfile",
  components: { TwootItem },
  data() {
    return {
      newTwootContent: "",
      selectedTwootType: "instant",
      twootTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Twoot" },
      ],
      followers: 20000000,
      user: {
        id: 1,
        username: "_AlbertoDinca",
        firstName: "Alberto",
        lastName: "Dinca",
        email: "d_alberto9@yahoo.com",
        isAdmin: true,
        twoots: [
          {
            id: 1,
            content: "Twotter 2 is better than 1",
          },
          {
            id: 2,
            content: "Twotter 2 is better than 1 cause 1 doesn't exist",
          },
          {
            id: 3,
            content: "Ciarpili",
          },
          {
            id: 4,
            content: "WWWWWW",
          },
        ],
      },
    };
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower`);
      }
    },
  },
  computed: {
    newTwootCharacterCount() {
      return this.newTwootContent.length;
    },
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
    userid() {
      return useRoute.params.userid;
    },
  },
  methods: {
    toggleFavourite(id) {
      console.log(`Favourited Tweet #${id}`);
    },

    createNewTwoot() {
      if (this.newTwootContent && this.selectedTwootType !== "draft") {
        this.user.twoots.unshift({
          id: this.user.twoots.length + 1,
          content: this.newTwootContent,
        });
        this.newTwootContent = "";
      }
    },

    followUser() {
      this.followers++;
    },
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style lang="scss" scoped>
.navbar {
  display: block;
  background: rebeccapurple;
  height: 50px;
  width: 100%;
  .navbar-logo {
    color: white;
    font-size: 2em;
    position: relative;
    top: 10px;
    left: 10px;
  }
  .navbar-username {
    position: relative;
    font-size: 2em;
    left: 86%;
    bottom: 55px;
    color: white;
  }
}
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;

  .user-profile_admin-badge {
    background: rebeccapurple;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0px 10px;
    font-weight: bold;
  }
  .user-profile_user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
  }
  .user-profile_create-twoot {
    display: flex;
    flex-direction: column;
    margin-top: 20px;
    border-top: 1px solid #dfe3e8;
    #newTwootType {
      margin-top: 10px;
    }
    &.--exceded {
      color: red;
      border: red;

      button {
        background: red;
        color: white;
      }
    }
  }
  .user-profile_twoot-button {
    margin-top: 10px;
    width: 35%;
    margin-left: 175px;
    border-radius: 5px;
    box-shadow: 0px 0px #000000;
    cursor: pointer;
  }
  h1 {
    margin: 0px;
  }
}
</style>
