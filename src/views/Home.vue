<template>
  <div class="home">
    <h1>Home - Welcome to Twotter</h1>
    <App />
  </div>
</template>

<script>
// @ is an alias to /src
import App from "../App.vue";

export default {
  name: "Home",
  components: {
    App,
  },
};
</script>
<style lang="scss" scoped>
.home {
  background: rebeccapurple;
  color: white;
}
</style>
