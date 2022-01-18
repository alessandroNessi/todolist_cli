<template>
  <div class="container-fluid" id="app">
    <div class="container d-flex" id="main__container">
      <div class="d-block div">ciao</div>
    </div>
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
};
</script>

<style lang="scss">
  @import "~bootstrap/dist/css/bootstrap.css";
  @import "./common/css/variabiles.css";
  #app {
    font-family: "Roboto", sans-serif;
    height: 100vh;
    background-color: var(--main-bg-color);
    // justify-content: center;
    #main__container{
      justify-content: center;
    }
    .div{
      width: 20px;
    }
  }
</style>
