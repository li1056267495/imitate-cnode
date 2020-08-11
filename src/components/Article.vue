<template>
  <div class="article">
    <!-- 如果正在加载显示加载动画 -->
    <div class="loading" v-if="isloading">
      <img src="../assets/loading.gif" alt />
    </div>
    <div v-else>
      <div class="topic_header">
        <!-- 标题 -->
        <div class="topic_title">{{ post.title }}</div>
        <ul>
          <li>•发布于：{{ post.create_at | formatDate }}</li>
          <li>•作者：{{ post.author.loginname }}</li>
          <li>•{{ post.visit_count }}次浏览</li>
          <li>•来自{{ post | tabFormatter }}</li>
        </ul>
        <!-- 内容 -->
        <div v-html="post.content" class="topic_content"></div>
      </div>
      <!-- 回复 -->
      <div class="reply">
        <div class="topbar">回复</div>
        <div
          v-for="(reply, index) in post.replies"
          :key="index"
          class="replySec"
        >
          <div class="replyUp">
            <router-link
              :to="{
                name: 'user_info',
                params: {
                  name: reply.author.loginname
                }
              }"
            >
              <img :src="reply.author.avatar_url" alt />
            </router-link>
            <router-link
              :to="{
                name: 'user_info',
                params: {
                  name: reply.author.loginname
                }
              }"
            >
              <span>{{ reply.author.loginname }}</span>
            </router-link>
            <span>{{ index + 1 }}楼</span>
            <span>
              <span v-if="reply.ups.length > 0" class="replyups"
                >☝{{ reply.ups.length }}</span
              >
              <span v-else></span>
            </span>
          </div>
          <p v-html="reply.content"></p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      isloading: false,
      posts: [] //代表当前文章页的所有内容
    };
  },
  methods: {
    getArticleData() {
      this.$http
        .get(`https://cnodejs.org/api/v1/topic/${this.$route.params.id}`)
        .then(res => {
          if (res.data.success === true) {
            this.isloading = false;
            this.post = res.data.data;
            console.log(res);
          }
        })
        .catch(err => {
          console.log(err);
        });
    }
  },
  beforeMount() {
    this.isloading = true;
    this.getArticleData();
  }
};
</script>
<style>
@import url("../assets/markdown-github.css");
.article {
  margin-top: 20px;
}
.loading {
  text-align: center;
  padding-top: 300px;
}
.reply,
.topic_header {
  background-color: #fff;
}
.replyUp img {
  width: 30px;
  height: 30px;
  position: relative;
  bottom: -9px;
}
a {
  color: #08c;
  text-decoration: none;
  font-size: 14px;
}

.topbar {
  padding: 10px 10px;
  background-color: #f6f6f6;
  height: 40px;
  font-size: 12px;
}

.article:not(:first-child) {
  margin-right: 340px;
  margin-top: 15px;
}

.reply {
  margin-top: 15px;
}
.reply p {
  font-size: 15px;
  line-height: 1.7em;
  overflow: auto;
  margin-bottom: 1em;
  padding: 4px 0;
}

.reply a,
.reply span {
  font-size: 13px;
  color: #666;
  text-decoration: none;
}
.replySec {
  border-bottom: 1px solid #e5e5e5;
  padding: 0 10px;
}

.loading {
  text-align: center;
}

.replyups {
  float: right;
  margin-top: 10px;
}

.topic_header {
  padding: 10px;
}

.topic_title {
  font-size: 20px;
  font-weight: bold;
  padding-top: 8px;
}

.topic_header ul {
  list-style: none;
  padding: 0px 0px;
  margin: 6px 0px;
}

.topic_header li {
  display: inline-block;
  font-size: 12px;
  color: #838383;
}

.topic_content {
  border-top: 1px solid #e5e5e5;
  padding: 0 10px;
  font-size: 15px;
  line-height: 2em;
  overflow: auto;
}

.markdown-text img {
  width: 92% !important;
}
</style>
