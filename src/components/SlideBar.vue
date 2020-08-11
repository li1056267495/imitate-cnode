<template>
  <div class="authorinfo">
    <div class="rightmsg">
      <ul>
        <!-- 作者信息 -->
        <li>
          <div class="authersummay">
            <div class="author">作者</div>
            <div class="authorloginname">
              <router-link
                :to="{
                  name: 'user_info',
                  params: {
                    name: userinfo.loginname
                  }
                }"
              >
                <img :src="userinfo.avatar_url" alt />
              </router-link>
              <div class="score">积分{{ userinfo.score }}</div>
            </div>
          </div>
        </li>
        <!-- 广告 -->
        <li>
          <div class="advertising">
            <a
              href="https://www.ucloud.cn/site/active/gift.html?utm_source=cnodejs&utm_medium=content_pic_pc_540_130&utm_campaign=huodong&utm_content=gift&ytag=cnodejs"
            >
              <img
                src="//static.cnodejs.org/FgIok2ZlDer2QOb8sJ20S9Y8T2Jq"
                alt
              />
            </a>
            <a
              href="https://www.qiniu.com/events/20200316?utm_campaign=20200316&utm_content=cnode&utm_medium=banner&utm_source=cnode&utm_term=cnode"
            >
              <img
                src="//static.cnodejs.org/FlajCCXkxZaOsuWp3k0iaiqfrJaS"
                alt
              />
            </a>
            <a href="https://www.aliyun.com/product/nodejs?ref=cnode">
              <img
                src="//static.cnodejs.org/Fn4D6BhOTz1IswvmzeZ1q7QW1ls_"
                alt
              />
            </a>
          </div>
        </li>
        <!-- 友情社区 -->
        <li>
          <div class="friendship">友情社区</div>
          <div class="comimg">
            <ul>
              <li>
                <a href="https://ruby-china.org/">
                  <img
                    src="//static2.cnodejs.org/public/images/ruby-china-20150529.png"
                    alt
                  />
                </a>
                <a href="https://learnku.com/laravel">
                  <img
                    src="//static2.cnodejs.org/public/images/phphub-logo.png"
                    alt
                  />
                </a>
              </li>
            </ul>
          </div>
        </li>
        <!-- 二维码 -->
        <li>
          <div class="qrcodetitle">客户端二维码</div>
          <div class="qrcode">
            <img src="//static.cnodejs.org/FtG0YVgQ6iginiLpf9W4_ShjiLfU" alt />
            <p>
              <a href="https://github.com/soliury/noder-react-native"
                >客户端源码地址</a
              >
            </p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: "SlideBar",
  data() {
    return {
      isloading: false,
      userinfo: {}
    };
  },
  methods: {
    getData() {
      this.$http
        .get(`https://cnodejs.org/api/v1/user/${this.$route.params.name}`)
        .then(res => {
          this.isloading = false;
          this.userinfo = res.data.data;
          console.log(res.data.data);
        })
        .catch(err => {
          console.log(err);
        });
    }
  },
  beforeMount() {
    this.isloading = true;
    this.getData();
  }
};
</script>
<style scoped>
.authorinfo {
  margin-left: 20px;
}
.loading {
  text-align: center;
  padding-top: 300px;
}
img {
  width: 48px;
  height: 48px;
}
.rightmsg ul {
  list-style: none;
  margin-top: 20px;
}
.rightmsg ul li {
  width: 290px;
  margin-top: 20px;
  border-radius: 3px;
  padding: 10px;
  font-size: 14px;
  font-family: "Helvetica Neue", "Luxi Sans", "DejaVu Sans", Tahoma,
    "Hiragino Sans GB", STHeiti, sans-serif !important;
  font-weight: 400;
  background-color: white;
}
.author {
  width: 290px;
  margin-top: -10px;
  margin-left: -10px;
  color: #444;
  font-size: 14px;
  padding: 10px;
  background-color: #f6f6f6;
  border-radius: 3px 3px 0 0;
}
.authorloginname img {
  margin-top: 10px;
}
.score {
  margin-top: 10px;
}
.advertising {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: -10px;
}
.advertising img {
  width: 270px;
  height: 65px;
  margin-top: 10px;
  cursor: pointer;
}
.integration,
.friendship,
.qrcodetitle {
  background-color: #f5f5f5;
  width: 290px;
  margin-left: -10px;
  margin-top: -10px;
  padding: 10px 20px;
  font-size: 13px;
  color: #444;
}
.comimg ul {
  display: flex;
  margin-top: -20px;
}
.comimg ul li img {
  width: 150px;
  margin-top: 10px;

  height: 50px;
  cursor: pointer;
}
.qrcode img {
  width: 200px;
  height: 200px;
  margin-top: 10px;
  margin-left: 50%;
  transform: translate(-50%, 0);
}
.qrcode p {
  margin-top: 10px;
  margin-left: 56%;
  transform: translate(-50%, 0);
  color: #cccccc;
}
.qrcode a {
  text-decoration: none;
  color: #778087;
  font-size: 13px;
  text-shadow: nonr;
}
</style>
