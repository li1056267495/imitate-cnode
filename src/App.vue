<template>
  <div id="app">
    <Header />
    <div class="main">
      <router-view name="otherMain"></router-view>
      <router-view name="bodyMain"></router-view>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header";
import PostList from "./components/PostList";
export default {
  name: "App",
  components: {
    Header,
    PostList,
  },
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
  width: 80%;
  margin: 0 auto;
}
</style>
