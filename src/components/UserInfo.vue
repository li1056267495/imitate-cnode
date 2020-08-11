<template>
  <div class="UserInfo">
    <!-- 在数据未加载前，加载动态图片 -->
    <div class="loading" v-if="isloading">
      <img src="../assets/loading.gif" alt />
    </div>
    <div class="userInformasion" v-else>
      <div class="userheader">
        <router-link :to="{name:'root'}">
          <div class="roottopic">主页/</div>
        </router-link>
        <div class="rootpage">
          <div class="rootimg">
            <img :src="userinfo.avatar_url" />
          </div>
          <div class="loginname">{{userinfo.loginname}}</div>
        </div>
        <p class="score">{{userinfo.score}}积分</p>
        <p class="createtime">注册时间{{userinfo.create_at|formatDate}}</p>
      </div>
      <div class="userbody">
        <div class="clearlytopic">最近创建的话题</div>
        <div class="topiclist">
          <ul>
            <li v-for="(item ,index) in userinfo.recent_replies" :key="index">
              <img :src="userinfo.avatar_url" alt />
              <router-link
                :to="{name:'post_content',params:{
                  id:item.id
              }}"
              >
                <p>{{item.title}}</p>
              </router-link>
            </li>
          </ul>
        </div>
      </div>
      <div class="userfooter">
        <div class="clearlycreate">最近参与的话题</div>
        <div class="createlist">
          <ul>
            <li v-for="(item ,index) in userinfo.recent_topics" :key="index">
              <router-link
                :to="{name:'post_content',params:{
                  id:item.id
              }}"
              >{{item.title}}</router-link>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "UserInfor",
  data() {
    return {
      isloading: false,
      userinfo: {},
    };
  },
  methods: {
    getData() {
      this.$http
        .get(`https://cnodejs.org/api/v1/user/${this.$route.params.name}`)
        .then((res) => {
          this.isloading = false;
          this.userinfo = res.data.data;
          console.log(res.data.data);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  beforeMount() {
    this.isloading = true;
    this.getData();
  },
};
</script>
<style scoped>
.UserInfo {
  font-family: "Helvetica Neue", "Luxi Sans", "DejaVu Sans", Tahoma,
    "Hiragino Sans GB", STHeiti, sans-serif !important;
}
a {
  text-decoration: none;
  color: #08c;
}
a:hover {
  color: #005580;
  text-decoration: underline;
}
.loading {
  text-align: center;
  padding-top: 300px;
}
.userheader {
  margin-top: 20px;
  background: white;
  border-radius: 3px;
}
.roottopic {
  padding: 10px;
  background-color: #f6f6f6;
  border-radius: 3px 3px 0 0;
  font-size: 14px;
  color: #80bd01;
}
.rootpage {
  display: flex;
  padding: 10px 10px;
}
.rootimg img {
  width: 40px;
  height: 40px;
  border-radius: 3px;
}
.loginname {
  margin-left: 10px;
  line-height: 2em;
  color: #778087;
  font-size: 14px;
}
.score {
  margin-left: 10px;
  font-size: 14px;
  line-height: 2em;
}
.createtime {
  margin-left: 10px;
  color: #ababab;
  font-size: 14px;
  line-height: 2em;
}

.userbody {
  margin-top: 20px;
  background: white;
  border-radius: 3px;
}
.clearlytopic,
.clearlycreate {
  color: #444;
  font-size: 14px;
  padding: 10px;
  background-color: #f6f6f6;
  border-radius: 3px 3px 0 0;
}
.userbody img {
  width: 30px;
  height: 30px;
  border-radius: 3px;
}
.topiclist ul li {
  display: flex;
  justify-content: start;
  align-items: center;
  padding: 10px 10px;
}
.topiclist ul li p {
  margin-left: 10px;
}
.userfooter {
  margin-top: 20px;
  background: white;
  border-radius: 3px;
}
.createlist ul li {
  display: flex;
  justify-content: start;
  align-items: center;
  padding: 10px 10px;
}
</style>