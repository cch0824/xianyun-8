<template>
  <div class="traVeldiary">
    <el-row :gutter="20">
      <!-- 左边 -->
      <el-col :span="20">
        <div class="grid-content-left bg-purple">
          <span>发表新攻略</span>
          <p>分享你的个人游记,让更多人看到你哦!</p>
          <el-input v-model="input" placeholder="请输入标题" class="plesepayBiaoti"></el-input>
          <!-- 富文本框 -->
          <div class="quilll" v-quill></div>

          <!-- 选择城市 -->
          <em>选择城市</em>
          <el-autocomplete
            v-model="state"
            placeholder="请搜索游玩城市"
            @select="seleCity"
            :fetch-suggestions="querySearchAsync"
          ></el-autocomplete>

          <div class="iuuserNe">
            <i @click="iusseNews">发布</i>
            <i>或者</i>
            <i>保存到草稿</i>
          </div>
        </div>
      </el-col>

      <!-- 右边 -->
      <el-col :span="4">
        <div class="grid-content-right bg-purple">草稿箱(0)</div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: "",
      state: ""
    };
  },
  methods: {
    //点击发布
    iusseNews() {

    },
    //选择城市
    seleCity() {

    },
    //输入框输入值的时候触发的事件
    querySearchAsync(value, cb) {
      this.$axios({
        url: "/cities",
        params: {
          name: this.state
        }
      }).then(res => {
         console.log(res);
      });
    }
  },
  mounted() {}
};
</script>

<style scoped lang='less'>
.traVeldiary {
  width: 1000px;
  margin: 25px auto;
  .grid-content-left {
    width: 750px;
    span {
      font-size: 23px;
    }
    p {
      font-size: 12px;
      color: #ccc;
      margin: 10px 0;
    }
  }

  //   右边
  .grid-content-right {
    border: 1px solid #ccc;
    padding: 10px;
  }
}

//富文本框
.quilll {
  height: 350px;
}
.plesepayBiaoti {
  margin-bottom: 20px;
}
.el-autocomplete {
  margin: 20px auto;
}
.iuuserNe :nth-child(1) {
  background-color: #66b1ff;
  color: #fff;
  font-size: 13px;
  padding: 7px 15px;
  border-radius: 5px;
}
.iuuserNe :nth-child(3) {
  color: #ffa500;
}
</style>
