<template>
  <div class="container-fluid app py-4" id="app">
    <div class="container d-flex" id="main__container">
      <Header title="TodoList"></Header>
      <Main></Main>
      <Footer></Footer>
    </div>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  components: {
    // HelloWorld,
    Header,
    Main,
    Footer,
  },
};
</script>

<style lang="scss">
@import "~bootstrap/dist/css/bootstrap.css";
@import "./common/css/variabiles.css";
@import "./common/css/common.css";
.app {
  font-family: "Roboto", sans-serif;
  background-image: url('./common/images/bgr.jpg');
  background-size: cover;
  background-position: center;
  height: 100vh;
  *{
    background-color: var(--main-bg-color);
  }
  #main__container {
    background-color: var(--main-container-bg-color);
    box-shadow: 0 0 3px 3px var(--main-container-bg-color);
    backdrop-filter: blur(6px);
    border-radius: 0.5rem;
    flex-direction: column;
    justify-content: center;
    max-width: var(--max-width);
  }
}
</style>
