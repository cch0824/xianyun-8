<template>
  <div class="user">
    <span>{{data&&data.account&&data.account.nickname}}</span>
    <i>{{data&&data.account&&data.account.updated_at|gettimer}}</i>
    <span class="level">{{data.level}}</span>
    <p class="text">{{data&&data.content}}</p>
    <img
      class="commImg"
      v-for="(pic, index2) in data.pics"
      :key="index2"
      :src="$axios.defaults.baseURL +pic.url"
    />
    <nuxt-link to="#" @click="toreply(data)" class="reply">回复</nuxt-link>
    <items v-if="data.parent" :data="data.parent" />
  </div>
</template>

<script>
import moment from "moment";

export default {
  props: {
    data: {
      type: Object,
      default: { account: {}, parent: {} }
    }
  },
  name: "items",
  data() {
    return {};
  },
  methods: {
    // 回复评论
    toreply(data) {
      console.log(data);
    }
  },
  filters: {
    gettimer: timer => {
      let newdate = moment(timer).format("YYYY-MM-DD HH:mm");
      return newdate;
    }
  }
};
</script>

<style lang="less" scoped>
p {
  padding-left: 20px;
}
.text {
  font-size: 16px;
  color: #333;
  text-align: left;
}
.second {
  margin: 10px 0 0px 20px;
  padding: 8px;
  border: 1px solid #ccc;
  background-color: #f9f9f9;
}
span {
  font-size: 12px;
  color: #666;
}
i {
  font-size: 12px;
  color: #999;
}
.reply {
  float: right;
  font-size: 12px;
  color: #666;
  margin-top: -7px;
  color: #1e50a2;
}
.commImg {
  width: 100px;
  height: 100px;
}
</style>