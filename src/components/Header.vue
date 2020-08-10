<template>
  <div class="header">
    <div class="headermain">
      <img src="//static2.cnodejs.org/public/images/cnodejs_light.svg" alt />
      <ul>
        <li>
          <a href="#">首页</a>
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
* {
  margin: 0;
  padding: 0;
  box-sizing: bo;
}
.header {
  background: rgb(68, 68, 68);
  height: 50px;
}
.headermain {
  max-width: 1358px;
  margin: 0 auto;
}
img {
  max-width: 120px;
  margin-left: 15px;
  margin-top: 10px;
}
a {
  text-decoration: none;
  color: #cccccc;
  font-size: 12px;
  text-shadow: nonr;
}
ul {
  list-style: none;
  float: right;
  display: flex;
  margin-top: 4px;
}
li {
  list-style: none;
  padding: 10px 15px;
}
</style>