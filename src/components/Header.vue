<template>
  <div class="header">
    <div class="headermain">
      <img src="//static2.cnodejs.org/public/images/cnodejs_light.svg" alt />
      <input type="text" class="search" />
      <ul>
        <li>
          <a href="/">首页</a>
        </li>
        <li>
          <a href="#">新手入门</a>
        </li>
        <li>
          <a href="#">API</a>
        </li>
        <li>
          <a href="#">关于</a>
        </li>
        <li>
          <a href="#">注册</a>
        </li>
        <li>
          <a href="#">登录</a>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: "Header",
};
</script>
<style scoped>
.header {
  background: rgb(68, 68, 68);
  height: 50px;
}
.headermain {
  display: flex;
  max-width: 1358px;
  margin: 0 auto;
}
img {
  max-width: 120px;
  margin-left: 15px;
}
a {
  text-decoration: none;
  color: #cccccc;
  font-size: 12px;
  text-shadow: nonr;
}
a:hover {
  color: aliceblue;
}
ul {
  margin-left: 600px;
  list-style: none;
  display: flex;
  margin-top: 4px;
}
li {
  list-style: none;
  padding: 10px 15px;
}
.search {
  outline: none;
  margin-left: 26px;
  margin-top: 12px;
  border: 1px solid red;
  width: 240px;
  height: 26px;
  background: 4px 4px no-repeat #888;
  padding: 3px 5px 3px 10px;
  color: #666;
  border: 0;
  border-radius: 20px;
  transition: all 0.5s;
}
.search:hover {
  background: white;
  transition: all 0.5s;
}
</style>