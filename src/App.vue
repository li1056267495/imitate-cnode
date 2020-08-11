<template>
  <div id="app">
    <Header />
    <div class="main">
      <router-view name="bodyMain"></router-view>
      <router-view name="otherMain"></router-view>
    </div>
    <Footer class="footer" />
  </div>
</template>

<script>
import Header from "./components/Header";
import PostList from "./components/PostList";
import Footer from "./components/Footer";
export default {
  name: "App",
  components: {
    Header,
    PostList,
    Footer
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
ul,
li {
  list-style: none;
}
#app {
  background: #e1e1e1;
}
.main {
  display: flex;
  width: 80%;
  margin: 0 auto;
}
.footer {
  margin-top: 20px;
}
</style>
