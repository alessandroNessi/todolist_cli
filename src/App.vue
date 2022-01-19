<template>
  <div class="container-fluid p-5" id="app">
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
#app {
  font-family: "Roboto", sans-serif;
  background-color: var(--green-opacity-color);
  height: 100vh;
  *{
    background-color: var(--main-bg-color);
  }
  #main__container {
    flex-direction: column;
    justify-content: center;
    max-width: var(--max-width);
  }
}
</style>
