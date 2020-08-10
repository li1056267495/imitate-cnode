<template>
  <div class="posts">
    <!-- 在数据未加载前，加载动态图片 -->
    <div class="loading" v-if="isloading">
      <img src="../assets/jiazai.gif" alt />
    </div>
    <!-- 主题帖子列表 -->
    <div class="posttitle" v-else>
      <ul>
        <li>
          <div class="tobar">
            <span>全部</span>
            <span>精华</span>
            <span>分享</span>
            <span>问答</span>
            <span>招聘</span>
          </div>
        </li>
        <li v-for="(post, index) in posts" :key="index">
          <!-- 头像 -->
          <img :src="post.author.avatar_url" alt />
          <span class="allcount">
            <!-- 回复量/浏览量 -->
            <span class="reply_count">{{ post.reply_count }}</span>
            /{{ post.visit_count }}
          </span>
          <!-- 帖子的分类：置顶，精华，其他 -->
          <span
            :class="[
              {
                put_good: (post.good === true),
                put_top: (post.top === true),
                topiclist: (post.good !== true && post.top !== true)
              }
            ]"
          >
            <span>{{ post | tabFormatter }}</span>
          </span>
          <!-- 标题 -->
          <router-link
            :to="{
            name:'post_content',
            params:{
              id:post.id
            }
            }"
          >
            <span class="title">
              <span>{{ post.title }}</span>
            </span>
          </router-link>

          <!-- 时间 -->
          <span class="last_reply">{{ post.last_reply_at | formatDate }}</span>
        </li>
      </ul>
    </div>
    <!-- 右侧信息 -->
    <div class="rightmsg">
      <ul>
        <!-- 社区 -->
        <li>
          <div class="community">
            <p class="font1">CNode：Node.js专业中文社区</p>
            <p class="font2">
              您可以
              <a href>登录</a>或
              <a href>注册</a>，也可以
            </p>
            <p class="font3">通过 GitHub 登录</p>
          </div>
        </li>
        <!-- 广告 -->
        <li>
          <div class="advertising">
            <a
              href="https://www.ucloud.cn/site/active/gift.html?utm_source=cnodejs&utm_medium=content_pic_pc_540_130&utm_campaign=huodong&utm_content=gift&ytag=cnodejs"
            >
              <img src="//static.cnodejs.org/FgIok2ZlDer2QOb8sJ20S9Y8T2Jq" alt />
            </a>
            <a
              href="https://www.qiniu.com/events/20200316?utm_campaign=20200316&utm_content=cnode&utm_medium=banner&utm_source=cnode&utm_term=cnode"
            >
              <img src="//static.cnodejs.org/FlajCCXkxZaOsuWp3k0iaiqfrJaS" alt />
            </a>
            <a href="https://www.aliyun.com/product/nodejs?ref=cnode">
              <img src="//static.cnodejs.org/Fn4D6BhOTz1IswvmzeZ1q7QW1ls_" alt />
            </a>
          </div>
        </li>
        <!-- 话题 -->
        <li>
          <div class="p1">
            <p>无人回复的话题</p>
          </div>
          <div class="p2">
            <p>nodejs应用层线程池</p>
            <p>分享【Java架构师成长直通车】</p>
            <p>请教有没有做过”通过充值Q币，再用Q...</p>
            <p>前端有没有好用的自定义图片标记插件？</p>
            <p>element-ui中的tree组件拖拽怎么实现复制</p>
          </div>
        </li>
        <!-- 积分榜 -->
        <li>
          <div class="integration">积分榜 TOP100 >></div>
          <div class="nameNum">
            <ul>
              <li v-for="(num,index) in nums" :key="index">
                <span class="num1">{{num.key}}</span>
                <span class="num2">{{num.name}}</span>
              </li>
            </ul>
          </div>
        </li>
        <!-- 友情社区 -->
        <li>
          <div class="friendship">友情社区</div>
          <div class="comimg">
            <ul>
              <li>
                <a href="https://ruby-china.org/">
                  <img src="//static2.cnodejs.org/public/images/ruby-china-20150529.png" alt />
                </a>
                <a href="https://learnku.com/laravel">
                  <img src="//static2.cnodejs.org/public/images/phphub-logo.png" alt />
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
              <a href="https://github.com/soliury/noder-react-native">客户端源码地址</a>
            </p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: "PostList",
  data() {
    return {
      isloading: false,
      posts: [],
      nums: [
        {
          key: "22385",
          name: "i5ting",
        },
        {
          key: "15820",
          name: "alsotang",
        },
        {
          key: "9800",
          name: "atian25",
        },
        {
          key: "9350",
          name: "leapon",
        },
        {
          key: "8780",
          name: "jiyinyiyong",
        },
        {
          key: "7485",
          name: "yakczh",
        },
        {
          key: "6855",
          name: "im-here",
        },
        {
          key: "6120",
          name: "DevinXian",
        },
        {
          key: "5815",
          name: "chapgaga",
        },
        {
          key: "5375",
          name: "magicdawn",
        },
      ],
    };
  },
  methods: {
    getData() {
      this.$http
        .get("https://cnodejs.org/api/v1/topics", {
          params: {
            page: 1,
            limit: 40,
          },
        })
        .then((res) => {
          this.isloading = false;
          this.posts = res.data.data;
          console.log(res.data.data);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  beforeMount() {
    this.isloading = true; //加载成功之前，加载动画
    this.getData(); //加载页面之前，获取数据
  },
};
</script>
<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.loading img {
  width: 600px;
  height: 600px;
}
img {
  width: 30px;
  height: 30px;
  vertical-align: middle;
}
a {
  text-decoration: none;
  color: #778087;
  font-size: 13px;
  text-shadow: nonr;
}
.posts {
  background: #e1e1e1;
  display: flex;
  flex-wrap: nowrap;
  width: 1328px;
  margin-left: 50%;
  transform: translate(-50%, 0);
}

.posttitle ul {
  width: 1016px;
  list-style: none;
  margin-top: 20px;
}
.posttitle li:not(:first-child) {
  padding: 9px;
  font-size: 15px;
  font-family: "Helvetica Neue", "Luxi Sans", "DejaVu Sans", Tahoma,
    "Hiragino Sans GB", STHeiti, sans-serif !important;
  font-weight: 400;
  background-color: white;
  color: #333;
  border-top: 1px solid #f0f0f0;
}

.posttitle li:not(:first-child):hover {
  background: #f5f5f5;
}

.posttitle li span {
  line-height: 30px;
}
.allcount {
  width: 70px;
  display: inline-block;
  text-align: center;
  font-size: 12px;
  color: rgb(183, 188, 196);
}
.reply_count {
  color: rgb(168, 120, 192);
  font-size: 14px;
}
.put_good,
.put_top {
  background: #80bd01;
  padding: 2px 4px;
  border-radius: 3px;
  -webkit-border-radius: 3px;
  -moz-border-radius: 3px;
  -o-border-radius: 3px;
  color: #fff;
  font-size: 12px;
  margin-right: 10px;
}
.topiclist {
  background-color: #e5e5e5;
  color: #999;
  padding: 2px 4px;
  border-radius: 3px;
  -webkit-border-radius: 3px;
  -moz-border-radius: 3px;
  -o-border-radius: 3px;
  font-size: 12px;
  margin-right: 10px;
}
.last_reply {
  text-align: right;
  min-width: 50px;
  white-space: nowrap;
  float: right;
  color: #778087;
  font-size: 12px;
}

.tobar {
  padding: 4px 0;
  background-color: #f5f5f5;
}

.tobar span {
  font-size: 14px;
  color: #80bd01;
  line-height: 40px;
  margin: 0 10px;
  cursor: pointer;
  vertical-align: middle;
}
.tobar span:hover {
  color: rgb(0, 85, 157);
}
.rightmsg ul {
  list-style: none;
  margin-top: 20px;
  margin-left: 20px;
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
.community {
  background: white;
  line-height: 30px;
  padding: 14px 0;
}
.community p {
  margin-left: 14px;
}
.community .font1 {
  font-size: 16px;
}
.community .font2 {
  font-size: 12px;
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
.p2 {
  width: 290px;
  cursor: pointer;
  padding: 0 10px;
  line-height: 30px;
  color: rgb(140, 128, 150);
}
.p1 {
  background: rgb(246, 246, 246);
  width: 290px;
  margin-left: -10px;
  margin-top: -10px;
  padding: 10px 20px;
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
.nameNum {
  margin-top: -20px;
}
.num1 {
  margin-left: 10px;
}
.num2 {
  margin-left: 20px;
  cursor: pointer;
}
.nameNum ul li {
  margin-left: -30px;
  margin-top: -6px;
  color: rgb(128, 128, 159);
}

.comimg ul {
  display: flex;
  margin-top: -20px;
}
.comimg ul li img {
  width: 150px;
  margin-top: 10px;
  margin-left: -20px;
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
</style>
