<template>
  <div class="pagination">
    <div class="pages">
      <button @click="changeBtn">首页</button>
      <button @click="changeBtn">上一页</button>
      <button v-if="ishowbtn">...</button>
      <button
        v-for="(btn, index) in pagebtns"
        :key="index"
        :class="[{ pagechange: btn === currentPage }, 'pagebtn']"
        @click="changeBtn(btn)"
      >
        {{ btn }}
      </button>
      <button @click="changeBtn">下一页</button>
    </div>
  </div>
</template>
<script>
import $ from "jquery";
export default {
  name: "Pagination",
  data() {
    return {
      ishowbtn: false,
      pagebtns: [1, 2, 3, 4, 5, "..."],
      currentPage: 1
    };
  },
  methods: {
    changeBtn(value) {
      //点击上一页，下一页
      if (typeof value !== "number") {
        switch (value.target.innerText) {
          case "上一页":
            $("button.pagechange")
              .prev()
              .click();
            break;
          case "下一页":
            $("button.pagechange")
              .next()
              .click();
            break;
          case "首页":
            this.pagebtns = [1, 2, 3, 4, 5, "..."];
            this.changeBtn(1);
            break;
          default:
            break;
        }
        return;
      }
      this.currentPage = value;
      if (value > 4) {
        this.ishowbtn = true;
      } else {
        this.ishowbtn = false;
      }
      if (value === this.pagebtns[4]) {
        this.pagebtns.shift(); //移除第一个元素
        this.pagebtns.splice(4, 0, this.pagebtns[3] + 1); //添加最后一个
      } else if (value === this.pagebtns[0] && value !== 1) {
        this.pagebtns.unshift(this.pagebtns[0] - 1);
        this.pagebtns.splice(5, 1);
      }
      this.$emit("handleList", this.currentPage);
      console.log(this.currentPage);
    }
  }
};
</script>
<style scoped>
.pages {
  display: flex;
  align-content: center;
  justify-items: center;

  width: 1200px;
}
button {
  background: rgb(218, 218, 218);
  border-radius: 3px;
  outline: none;
  width: 50px;
  height: 30px;
  border: 1px solid rgb(241, 241, 241);
  cursor: pointer;
}
.pagechange {
  background: #80bd01;
}
</style>
