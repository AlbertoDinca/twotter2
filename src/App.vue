<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style lang="scss">
#app {
  font-family: Arial, Helvetica, sans-serif;
  color: #2c3e50;
  background-color: #f3f5fa;
}
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
}
</style>
